## 동기

상태 관리를 할 때 호환성 및 단순함을 이유로 외부의 글로벌 상태관리 라이브러리보다는 `React` 자체에 내장된 상태 관리 기능을 사용하는 것이 가장 좋다. 하지만 그것도 단점이 있다.

- 컴포넌트의 상태는 공통된 상위요소까지 끌어올림으로써 공유될 수 있지만, 이 과정에서 거대한 트리가 `Rerendering`되는 효과를 불러오기도 한다.
- `ContextAPI`는 단일 값만 저장할 수 있으며, 자체 소비자(consumer)를 가지는 여러 값들의 집합을 담을 수는 없다.
- 이 두가지 특성이 트리의 최상단(state가 존재하는 곳)부터 트리의 잎(state가 사용되는 곳)까지의 코드 분할을 어렵게한다.

`Recoil`은 API와 의미 및 동작을 가능한 `React`답게 유지하면서 이것을 개선하고자 한다.

`Recoil`은 직관적이지만 본질적인 방향 그래프를 정의하고 `React` 트리에 붙인다. 상태 변화는 이 그래프의 뿌리(`atoms`)로부터 순수함수(`selectors`)를 거쳐 컴포넌트로 흐른다.

## 주요 개념

### Atoms

`Atoms`는 상태의 단위이다. 그리고 상태의 업데이트와 구독이 가능하다. `atom`이 업데이트되면 각각의 구독된 컴포넌트는 새로운 값을 반영하여 `Rerendering`된다. `atoms`는 런타임에서 생성될 수도 있다. `Atoms`는 `React`의 로컬 컴포넌트의 상태 대신 사용할 수 있다. 동일한 `atom`이 여러 컴포넌트에서 사용되는 경우 모든 컴포넌트는 상태를 공유한다.

```javascript
const fontSizeState = atom({
  key: "fontSizeState",
  default: 14,
});
```

`Atoms`는 디버깅, 지속성 및 모든 `atoms`의 `map`을 볼 수 있는 `API`에 사용되는 고유한 `key`가 필요하다. 두개의 `atom`이 같은 키를 갖는 것은 오류이기 때문에 키값은 전역적으로 고유하도록 해야한다.
`React` 컴포넌트의 상태처럼 기본값도 가진다.

컴포넌트에서 `atom`을 읽고 쓰려면 `useRecoilState`라는 `Hook`을 사용한다. `React`의 `useState`와 비슷하지만 상태가 컴포넌트 간에 공유될 수 있다는 차이가 있다.

```jsx
function FontButton() {
  const [fontSize, setFontSize] = useRecoilState(fontSizeState);
  return (
    <button
      onClick={() => setFontSize((size) => size + 1)}
      style={{ fontSize }}
    >
      Click to Enlarge
    </button>
  );
}
```

버튼을 클릭하면 버튼의 글꼴 크기가 1만큼 증가하며, `fontSizeState atom`을 사용하는 다른 컴포넌트의 글꼴 크기도 같이 변화한다.

```jsx
function Text() {
  const [fontSize, setFontSize] = useRecoilState(fontSizeState);
  return <p style={{ fontSize }}>This text will increase in size too.</p>;
}
```

### Selectors

`Selector`는 `atoms`나 다른 `selectors`를 입력으로 받아들이는 순수 함수(`pure function`)다. 상위의 `atoms` 또는 `selectors`가 업데이트되면 하위의 `selector` 함수도 다시 실행된다. 컴포넌트들은 `selectors`를 `atoms`처럼 구독할 수 있으며 `selectors`가 변경되면 컴포넌트들도 `Rerendering`된다.

`Selectors`는 상태를 기반으로 하는 파생 데이터를 계산하는 데 사용된다. 최소한의 상태 집합만 `atoms`에 저장하고 다른 모든 파생되는 데이터는 `selectors`에 명시한 함수를 통해 효율적으로 계산함으로써 쓸모없는 상태의 보존을 방지한다.

`Selectors`는 어떤 컴포넌트가 자신을 필요로하는지, 또 자신은 어떤 상태에 의존하는지를 추적하기 때문에 이러한 함수적인 접근방식을 매우 효율적으로 만든다.

컴포넌트의 관점에서 보면 `selectors`와 `atoms`는 동일한 인터페이스를 가지므로 서로 대체할 수 있다.

`Selectors`는 `selector`함수를 사용해 정의한다.

```javascript
const fontSizeLabelState = selector({
  key: "fontSizeLabelState",
  get: ({ get }) => {
    const fontSize = get(fontSizeState);
    const unit = "px";

    return `${fontSize}${unit}`;
  },
});
```

`get` 속성은 계산될 함수다. 전달되는 `get` 인자를 통해 atoms와 다른 `selectors`에 접근할 수 있다. 다른 `atoms`나 `selectors`에 접근하면 자동으로 종속 관계가 생성되므로, 참조했던 다른 `atoms`나 `selectors`가 업데이트되면 이 함수도 다시 실행된다.

이 `fontSizeLabelState` 예시에서 selector는 `fontSizeState`라는 하나의 atom에 의존성을 갖는다. 개념적으로 `fontSizeLabelState` selector는 `fontSizeState`를 입력으로 사용하고 형식화된 글꼴 크기 레이블을 출력으로 반환하는 순수 함수처럼 동작한다.

`Selectors`는 `useRecoilValue()`를 사용해 읽을 수 있다. `useRecoilValue()`는 하나의 `atom`이나 `selector`를 인자로 받아 대응하는 값을 반환한다. `fontSizeLabelState` `selector`는 `writable`하지 않기 때문에 `useRecoilState()`를 이용하지 않는다.

```jsx
function FontButton() {
  const [fontSize, setFontSize] = useRecoilState(fontSizeState);
  const fontSizeLabel = useRecoilValue(fontSizeLabelState);

  return (
    <>
      <div>Current font size: ${fontSizeLabel}</div>

      <button onClick={setFontSize(fontSize + 1)} style={{ fontSize }}>
        Click to Enlarge
      </button>
    </>
  );
}
```

버튼를 클릭하면 버튼의 글꼴 크기가 증가하는 동시에 현재 글꼴 크기를 반영하도록 글꼴 크기 레이블을 업데이트하는 두 가지 작업이 수행된다.

**참고**
<a href="https://recoiljs.org/ko/docs/introduction/motivation/">Recoil 공식문서</a>
