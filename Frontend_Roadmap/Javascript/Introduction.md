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

<hr>

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

<hr>

## 숫자형 변수

대부분의 스크립트 언어의 숫자 자료형과 유사하다.
정수와 부동 소수점의 구분 없이 하나의 자료형으로 사용된다.

아래와 같은 값들을 사용할 수 있습니다.

```
40
-8
0
0.5
-3.2
0x1af // 16진수 표현법
0ab1  // 8진수 표현법
Infinity
-Infinity
```
`NaN`과 `Infinity`
`NaN`은 숫자가 아님을 의미하며 `Infinity`는 무한대를 의미한다.

`parseInt('blabla')`, `Math.sqrt(-1)` 등의 함수는 `NaN`을 반환하게 되며, `42 / 0` 처럼 무한대가 나오는 식은 `Infinity`를 반환한다.

<hr>

## 문자형 변수

`JavaScript`는 일반적인 문자열(String)을 지원하는 대부분의 언어들처럼 문자형 자료형을 지원한다.
> TMI) C언어는 문자열(String)을 지원하지 않는다. ㅋㅋ

자바스크립트에서는 `char`형이 존재하지 않아 `"` 혹은 `'`중 어떤 것으로 감싸도 문자열로 만들어진다.

```js
var a = "Hello";
var b = 'world';
var c = "Amazing language 'JavaScript'";
```
### 이스케이프 문자
자바스크립트에서는 문자열안에 여러 줄의 글을 입력할 수 없다.
만약 작성하면 오류가 발생한다.

```js
var myString = "first line
second line
third line";
```

대신 줄바꿈 이스케이프 문자열인 `\n`를 사용한다.

```js
var myString = "first line\nsecond line\nthird line";
```

### 문자열 연결
문자열끼리 이어 붙이거나, 문자열과 숫자 등을 이어 붙일때는 `+` 연산자를 사용한다.
엄격한 언어와는 달리, 서로 다른 타입의 변수를 이어 붙여도, 변수를 강제로 문자열로 변형하여 이어 붙이게 된다.

```js
> "a" + "b"
ab

> "my age is " + 20
my age is 20

> "today is " + new Date()
today is Sat Feb 11 2017 21:06:27 GMT+0900 (KST)
```

### 문자열 인덱싱
C언어에서 `char`형 배열에서 `[i]`를 사용해 하나의 문자에 접근했듯, 자바스크립트 문자열도 배열처럼 취급되어 인덱스 접근자(`[i]`)를 사용하여 각 문자에 접근할 수 있다.

<hr>

## 배열

`JavaScript`의 배열은 숫자형이나 문자열과 마찬가지로 일반적인 스크립트 언어와 크게 다른 것이 없습니다.
`C`나 `Java`와는 상당히 다른데, 동적 타입 언어의 특징상 배열에도 타입이 정해져있지 않는다.

배열은 `[]`나 `new Array()`로 생성하며, 크기의 제약이 없고, 하나의 배열에 서로 다른 타입의 변수가 들어갈 수 있다.

```js
var emptyArray = [];
var oddNumbers = [1, 3, 5, 7, 9];
var evenNumbers = new Array(2, 4, 6, 8, 10);
var mixedArr = ['a', 1, 'b', 3, new Date(), "today"];
```

항목에 접근시에는 fruits[1] 처럼 사용한다.

### 자주쓰는 속성과 메소드

#### 길이 (length)
```
var colors = ['red', 'blue'];
console.log(colors.length);
// 2
```

#### 맨 뒤에 항목 추가 (push)
```
colors.push('green');
// ['red', 'blue', 'green']
```

#### 맨 뒤의 항목 제거 (pop)
```
colors.pop(); // 함수의 반환값: green
// 배열의 값: ['red', 'blue']
```

#### 맨 앞에 항목 추가 (unshift)
```
colors.unshift('white');
// ['white', 'red', 'blue']
```

#### 맨 앞의 항목 제거 (shift)
```
colors.shift(); // 함수의 반환값: white
// ['red', 'blue']
```

#### 배열 내부 값의 위치 찾기 (indexOf)
```
console.log( colors.indexOf('red') );
// 0
```

#### 인덱스 위치에서부터 n개의 항목 제거 (splice(1, 2))
```
fruits = ['red', 'blue', 'green', 'yellow'];
var removedItem = fruits.splice(1, 2); // 1번 인덱스부터 2개 제거

// fruits: ['red', 'yellow']
// removedItem: ['blue', 'green']
```

<hr>

## 객체

`JavaScript`에서 **객체**는 매우 중요한 개념이다. `JavaScript`의 자료형은 `Primitive` 타입과 `Object` 타입이 있다고 했는데, 다시 말하면 `Primitive` 타입 이외의 모든 변수는 객체 타입이라는 말이다.

객체와 `Primitive(원시)` 타입의 가장 큰 차이점은 `Reference(참조)`에 있다.

원시 타입 변수는 다른 변수에 값을 할당하거나 함수 인자로 넘길 때, 값을 복사하여 전달하지만,
객체는 메모리 **주소**를 복사시키며 값 자체는 복사되지 않아 같은 객체를 참조하게 된다.

**배열**도 **객체**의 일부이며, 함수의 인자로 넘기거나 다른 변수에 참조시킬 수 있다.

`JavaScript`에서 좁은 의미의 객체는 `키-값` 형태의 쌍을 저장할 수 있는 딕셔너리를 의미한다.
아래는 샘플 JavaScript Object 이다.

```js
var me = {
	'name': 'young',
	'birth': 1996,
	'sex': 'm'
}
```
중괄호 `{}` 를 이용해 생성하며 `:` 과 `,`를 이용해 중괄호 내부에서 `키-값` 쌍을 설정할 수 있다.
`{}` 대신 `new Object()` 생성자 사용도 가능하며, 인덱스 접근자 `[i]`를 사용하여 `키-값`을 설정할 수도 있다.

```js
var me = {};
me['name'] = 'young';
me['birth'] = 1996;
me['sex'] = 'm';
```
프로퍼티 접근자 `.`을 사용하여 `property(키)`에 접근할 수도 있다.

```js
var me = { 'name': 'young' };
me.birth = 1996;
```

<hr>