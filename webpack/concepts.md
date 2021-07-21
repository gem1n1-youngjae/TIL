## webpack 개념

`webpack은` `JavaScript` 애플리케이션을 위한 모듈 번들러 이다. `webpack`이 애플리케이션을 처리할 때, 내부적으로는 프로젝트에 필요한 모든 모듈을 매핑하고 하나 이상의 번들을 생성하는 디펜던시 그래프를 만든다.

> webpack 버전 4.0.0 이후로는 프로젝트를 번들링하기 위한 설정 파일을 필요로 하지 않는다. 하지만 사용자 요구에 따라 기대 이상으로 유연하게 설정이 가능 하다.

## 핵심 개념

#### Entry

`entry` 속성은 웹팩에서 웹 자원을 변환하기 위해 필요한 최초 진입점이자 자바스크립트 파일 경로이다.

기본값은 ./src/index.js이지만, webpack 설정에서 entry 속성을 설정하여 다른 (또는 여러 엔트리 포인트)를 지정할 수 있다.

```js
module.exports = {
  entry: "./src/index.js",
};
```

> `entry` 속성에 지정된 파일에는 웹 애플리케이션의 전반적인 구조와 내용이 담겨져 있어야 한다. 또한, 웹팩이 해당 파일을 가지고 웹 애플리케이션에서 사용되는 모듈들의 연관 관계를 이해하고 분석하기 때문에 애플리케이션을 동작시킬 수 있는 내용들이 담겨져 있어야 한다.

#### Output

`output` 속성은 웹팩을 돌리고 난 결과물의 파일 경로를 의미한다. 기본 출력 파일의 경우에는 ./dist/main.js로 , 생성된 기타 파일의 경우에는 ./dist 폴더로 설정된다.

```js
module.exports = {
  entry: "./src/index.js",
  output: {
    filename: "./dist/main.js",
  },
};
```

`output` 속성은 `filename`을 지정해줘야 하며 일반적으로 `path` 속성을 함께 정의한다.
여기서 `filename`은 웹팩으로 빌드한 파일의 이름을 의미하고, `path` 속성은 해당 파일의 경로를 의미한다.

#### Loader

`webpack`은 기본적으로 `JavaScrip`t와 `JSON` 파일만 이해한다.
`Loader`는 웹팩이 웹 애플리케이션을 해석할 때 자바스크립트 파일이 아닌 웹 자원 (`HTML`, `CSS`, `Images`, `font` 등)들을 변환할 수 있도록 도와주는 속성이다.

```js
module.exports = {
  module: {
    rules: [],
  },
};
```

`entry`나 `output` 속성과는 다르게 `module`라는 이름을 사용한다.

`Loader`는 `webpack` 설정에 두 가지 속성을 가진다.

1. 변한이 필요한 파일(들)을 식별하는 **`test`** 속성
2. 변환을 수행하는데 사용되는 `Loader`를 가리키는 **`use`** 속성

```js
module.exports = {
  module: {
    rules: [
      {
        test: /\.css$/,
        use: ["css-loader"],
      },
    ],
  },
};
```

위 코드는 해당 프로젝트의 모든 CSS 파일에 대해서 CSS Loader를 적용하겠다는 코드이다.

#### Plugin

`plugin`은 웹팩의 기본적인 동작에 추가적인 기능을 제공하는 속성이다. `Loader`와 비교하면 `Loader`는 파일을 해석하고 변환하는 과정에 관여하는 반면, `plugin`은 해당 결과물의 형태를 바꾸는 역할을 한다고 보면 된다.

```js
module.exports = {
  plugins: [],
};
```

`plugin`을 사용하려면 `require ()`를 통해 `plugin`을 요청하고 `plugin` 배열에 추가해야 합니다. 대부분의 `plugin`은 옵션을 통해 사용자가 지정할 수 있다. 다른 목적으로 `plugin`을 여러 번 사용하도록 설정할 수 있으므로 `new` 연산자로 호출하여 `plugin`의 `instance`를 만들어야 한다.

```js
const webpack = require("webpack");
const HtmlWebpackPlugin = require("html-webpack-plugin");

module.exports = {
  module: {
    rules: [
      {
        test: /\.css$/,
        use: ["css-loader"],
      },
    ],
  },
  plugins: [new HtmlWebpackPlugin({ template: "./src/index.html" })],
};
```

<hr>

**참고**
<a href="https://webpack.kr/concepts/modules/">웹팩 공식문서</a>
<a href="https://joshua1988.github.io/webpack-guide/webpack/what-is-webpack.html">웹팩 핸드북</a>
