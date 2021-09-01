## Matcher

`Matcher`란 이거 맞아? 라고 물어보는 메서드이다.
기대한 값이 실제 반환된 값과 일치하는 지를 확인하는 작업을 진행한다.
`Jest`는 값을 테스트 할 때 `Matcher`를 사용한다.

> 기본적으로 테스트는 다음과 같이 일정한 패턴으로 작성한다.
>
> ```js
> test("테스트 설명", () => {
>   expect("검증 대상").toXxx("기대 결과");
> });
> ```
>
> `toXxx` 부분에서 사용되는 함수가 `Matcher`이다.

### 일반적인 Matchers

#### toBe

정확한 값 일치 여부 확인

```js
test("two plus two is four", () => {
  expect(2 + 2).toBe(4);
});
```

#### toEqual

객체(object)의 값 일치 여부 확인

```js
test("object assignment", () => {
  const data = { one: 1 };
  data["two"] = 2;
  expect(data).toEqual({ one: 1, two: 2 });
});
```

#### not

불일치 여부 확인

```js
test("adding positive numbers is not zero", () => {
  for (let a = 1; a < 10; a++) {
    for (let b = 1; b < 10; b++) {
      expect(a + b).not.toBe(0);
    }
  }
});
```

### 참/거짓

테스트에서 때때로 `undefined`, `null`, `false를` 구별해야 할 필요가 있지만, 이를 별도로 다루는 것을 원치 않을 때도 있다. `Jest`는 원하는 것에 대해 명시적이게 할 수 있는 `Helper`를 포함하고 있다.

- `toBeNull은` `null`에만 일치
- `toBeUndefined`는 `undefined`에만 일치
- `toBeDefined`는 `toBeUndefined`의 반대
- `toBeTruthy`는 `if` 구문이 `true`로 취급하는 모든 것과 일치
- `toBeFalsy`는 `if` 구문이 `false`로 취급하는 모든 것과 일치

```js
test("test null", () => {
  const n = null;
  expect(n).toBeNull(); // pass
  expect(n).toBeUndefined(); // fail
  expect(n).toBeDefined(); // fail
  expect(n).toBeTruthy(); // fail
  expect(n).toBeFalsy(); // pass
});
```

### 숫자

- `toBeGreaterThan` : 큰 숫자 여부 확인
- `toBeGreaterThanOrEqual` : 같거나 큰 숫자 여부 확인
- `toBeLessThan` : 작은 숫자 여부 확인
- `toBeLessThanOrEqual` : 같거나 작은 숫자 여부 확인

```js
test("2 + 2 = 4", () => {
  const value = 2 + 2;
  expect(value).toBeGreaterThan(3);
  expect(value).toBeGreaterThanOrEqual(3.5);
  expect(value).toBeLessThan(5);
  expect(value).toBeLessThanOrEqual(4.5);

  // toBe와 toEqual은 숫자에 동등하다.
  expect(value).toBe(4);
  expect(value).toEqual(4);
});
```

다만, 부동 소수점은 컴퓨터의 근본적인 특성상 소수점에서 정확도 차이가 날 수 밖에 없다.

> 0.1 + 0.2 = 3.0000000004 같은거...

그럴땐 `toBeCloseTo`를 사용해야한다.

```js
test("adding floating point numbers", () => {
  const value = 0.1 + 0.2;
  expect(value).toBeCloseTo(0.3); // pass
});
```

### 문자열

#### toMatch

`toMatch` 와 정규 표현식을 사용하면 편하게 검사할 수 있다.

```js
test("there is no I in team", () => {
  expect("team").not.toMatch(/I/);
});

test('but there is a "stop" in Christoph', () => {
  expect("Christoph").toMatch(/stop/);
});
```

### 배열과 iterable

#### toContain

`toContain`를 사용하여 `배열`이나 `iterable`이 특정 항목을 포함하는지 여부를 확인 할 수 있다.

```js
const shoppingList = [
  "diapers",
  "kleenex",
  "trash bags",
  "paper towels",
  "milk",
];

test("the shopping list test", () => {
  expect(shoppingList).toHaveLength(5);
  expect(shoppingList).toContain("milk");
  expect(new Set(shoppingList)).toContain("milk");
});

// string은 iterable이다.
test("string test", () => {
  const str = "hello";
  expect(str).toHaveLength(5);
  expect(str).toContain("o");
});
```
