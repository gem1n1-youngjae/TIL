## JavaScript?

`HTML`은 웹 사이트에서 화면에 표시되는 정보를 약속 한 것이며, `CSS`는 구체적으로 어떤 스타일로 요소가 표시 되는지를 정하는 규격이라고 할 수 있다.
`HTML` 과 `CSS`는 정적인 것만 할 수 있는 언어인데, 대표적으로 사용자의 반응에 따라 유동적으로 화면과 내용이 바뀌는 일은 처리할 수 없다.

`JavaScript`는 웹페이지를 동적으로 만들어주는 언어로, 객체 기반의 스크립트 프로그래밍 언어다.
단순히 규격을 나타내는 `HTML`과 `CSS`와 달리, 변수와 함수 등이 존재하는 프로그래밍 언어이며, 현재도 활발한 발전이 이루어지고 있다.

> **Java와는 거의 관계가 없습니다!! (이름만 따왔으며, 설계 근본부터 다름)**

`JavaScript`를 줄여서 `js`라고 하며 파일 확장자 또한 `.js`를 사용한다.

### 사용법

`CSS`와 비슷하게 `HTML`문서 내에 기술하거나 별도의 파일로 분리하여 사용한다.

```js
<!-- HTML 내에 기술 -->
<html>
<head>
	<script>
		document.write('JavaScript');
	</script>
</head>
<body>
</body>
</html>
```
```js
<!-- 외부 파일에서 불러오기 -->
<head>
	<script type="text/javascript" src="./JS파일위치.js"></script>
</head>
```

### 스크립트 언어
`JavaScript`는 스크립트 언어이자 인터프리터 방식이 사용되어, 컴파일 과정이 필요 없다.

브라우저에서 즉시 해석되어 실행되는데, 한 곳에서 만든 엔진을 사용하지 않기 때문에
브라우저마다 완전 동일한게 동작하다고 하기 어렵다.

개발 속도가 빠르고 문법이 간단하지만, 복잡한 프로그램을 만들기는 어렵다는 특징이 있다.

### 동적타입 언어
자바스크립트에에서는 개발자가 변수의 타입을 지정해주지 않는다.
정확히 말하면 변수의 값에 따라 인터프리터가 알아서 변수의 타입을 파악하고 값을 저장한다.

```js
var a = 10;
var b = 'K';

function main() {
	return 2;
}
```

### 주석
여러줄짜리 주석은 /*로 시작하여 */로 끝난다.
한줄짜리 주석은 // 를 사용한다.

```js
/*
 author @prev
*/

var a;
// var b;
```

## 자료형

`JavaScript`는 동적타입 언어라고 설명했다.
개발자는 변수의 타입을 미리 선언할 필요가 없으며, 브라우저가 자동으로 파악한다.

하지만 이는 외적으로 타입이 없는 것 뿐이지, 내부적으로는 엄연히 자료형이 존재한다.

`JavaScript` 자료형은 크게 `Primitive(기본형)`과 `Object(객체)` 타입이 존재한다.

#### Primitive 타입 자료형
- `Boolean`: 논리적인 요소로, true와 false값이 있음
- `null`: 빈 값의 리터럴 표현
- `undefined`: 값을 할당하지 않은 변수가 가지는 값
- `Number`: 숫자형으로 정수와 부동 소수점, 무한대 및 NaN(숫자가 아님)값을 포함한다.
- `String`: 문자열

#### Object 타입 자료형
`Reference` 타입이라고도 한다.
`Object` 클래스 뿐만 아니라, **배열**과 **함수**, 사용자 정의 **클래스**도 모두 `Object`에 포함된다.

## 숫자형 변수