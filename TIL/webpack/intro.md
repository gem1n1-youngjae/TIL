## Webpack 등장 배경

웹페이지를 구축하다 보면은 `.html`, `css`, `.js`, `.png`와 같은 수많은 타입들이 생겨난다. 우리가 완성된 웹사이트를 로딩해보면 정말 많은 파일들이 다운로드 된다. 그러면 서버와의 접속이 많아지고 어플리케이션은 느리게 로딩되서 접속하는데 드는 비용이 많아진다.

또한, 많은 자바스크립트 패키지를 사용하다 보면 각각의 서로다른 패키지들이 같은 이름의 변수나 함수를 사용하면서 예상하지 못한 충돌로 오류가 발생하게 된다.

이런 문제들을 해결하기 위해서 등장한 도구들을 `Bundler`라고 부른다
`Bundler - 묶는다` 라는 사전적 의미를 가지고 있다.

즉 "<u>여러 개의 파일을 묶어주는 도구</u>" 라는 뜻이다.

대표적으로 `WebPack`, `Browserify`, `Parcel`이 Bundler에 속한다.

## Webpack

#### 웹팩이란?

웹팩은 가장 인기있고 많이 사용되는 (정적)모듈 번들러이다.

> 모듈 번들러란 웹 애플리케이션을 구성하는 자원(HTML, CSS, Javscript, Images 등)을 모두 각각의 모듈로 보고 이를 조합해서 병합된 하나의 결과물을 만드는 도구를 의미한다.

#### 모듈이란?

모듈이란 프로그래밍 관점에서 특정 기능을 갖는 작은 코드 단위를 의미한다.

```js
function sum(a, b) {
  return a + b;
}

function substract(a, b) {
  return a - b;
}

const pi = 3.14;

export { sum, substract, pi };
```

위 코드는 아래와 같이 3가지 기능을 갖고 있는 모듈이다.

- 두 숫자의 합을 구하는 `sum()` 함수
- 두 숫자의 차를 구하는 `substract()` 함수
- 원주율 값을 갖는 `pi` 상수

이처럼 성격이 비슷한 기능들을 하나의 의미 있는 파일로 관리하면 모듈된다.

#### 웹팩에서 모듈

웹팩에서 지칭하는 모듈이라는 개념은 위와 같이 자바스크립트 모듈에만 국한되지 않고 웹 애플리케이션을 구성하는 모든 자원을 의미힌다. 웹 애플리케이션을 제작하려면 `HTML`, `CSS`, `Javascript`, `Images`, `Font` 등 많은 파일들이 필하다. <u>이 파일 하나하나가 모두 모듈이다.</u>

#### 모듈 번들링이란?

그림과 같이 웹 애플리케이션을 구성하는 몇십, 몇백개의 자원들을 하나의 파일로 병합 및 압축 해주는 동작을 모듈 번들링이라고 한다.

<img src="https://joshua1988.github.io/webpack-guide/assets/img/webpack-bundling.e79747a1.png">

<hr/>

**참고**
<a href="https://webpack.kr/concepts/modules/">웹팩 공식문서</a>
<a href="https://joshua1988.github.io/webpack-guide/webpack/what-is-webpack.html">웹팩 핸드북</a>
<a href="https://opentutorials.org/module/4566">Opentutorials Webpack</a>
