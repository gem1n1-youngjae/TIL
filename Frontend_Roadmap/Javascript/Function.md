## 함수

`JavaScript`의 함수는 리턴 타입을 명시하지 않는다.
`function` 키워드로 함수를 선언하며, 괄호 안에서 매개변수를 받으며(변수 타입은 명시하지 않음), `return`을 통해 값을 반환한다.

```js
function plus(a, b) {
	var sum = a + b;
	return sum;
}
```
호출시에는 함수 이름과 괄호를 사용하여 호출한다.

```js
plus(3, 5);
```

### 함수의 범위
JavaScript 함수 내부에서 선언한 변수는 외부에서 참조할 수 없다.  
함수안에 함수 선언또한 가능한데, 이 경우에도 외부의 함수에서 내부의 변수를 참조할 수는 없다.

```js
function myFunc() {
	var myVar = 10;
	return a;
}
console.log( myFunc() ); // 10
console.log( myVar ); // undefined

```

```js
function outerFunc() {
	var outerVar = 'a';

	function innerFunc() {
		var innerVar = 'b';
		console.log(outerVar); // a
		console.log(innerVar); // b
	}
	innerFunc();

	console.log(outerVar); // a
	console.log(innerVar); // undefined
}

outerFunc();
```

## first-class object
`JavaScript`에서 함수는 일반적인 언어와 달리 **독특한 점**을 가지고 있다.

> JavaScript에서 함수는 first-class object(citizen)로 취급된다.

`first-class object`란 다음과 같은 조건을 만족하는 객체를 말한다.

- 변수나 데이터 구조안에 담을 수 있다.
- 파라미터로 전달 할 수 있다.
- 반환값(return value)으로 사용할 수 있다.
- 할당에 사용된 이름과 관계없이 고유한 구별이 가능하다.
- 동적으로 프로퍼티 할당이 가능하다.

자바스크립트에서 일반적으로 사용되는 `객체 변수`는 모두 `first-class object`라고 볼 수 있는데, 
**함수**조차 이와 같은 객체로 취급된다.


이러한 특성으로 인해 자바스크립트에서 함수 선언을 다음처럼 할 수도 있다.

```js
var plusFunc = function (a, b) {
	return a + b;
};
// 익명의 함수를 만들고 plusFunc 변수에 대입

plusFunc(3, 5);
```

아래처럼 함수에서 함수 자체를 반환하는 것도 가능하다.

```js
function a(x) {
	var b = function(y) {
		return x + y;
	};
	return b;
}

a(3)(4); // 7 반환
```

함수를 객체의 프로퍼티로도 사용할 수도 있다.

```js
var jacob = {
	'age': 18,
	'run': function() {
		alert('Jacob is running');
	},
	'sleep': function() {
		alert('Jacob sleeps');
	},
};
```

## 즉시 실행 함수
자바스크립트는 원래 네임스페이스 개념이 없다.  
하지만 함수의 클로저(범위) 개념과 first-class object 개념을 이용하면 비슷한 효과를 낼 수 있다.

```js
(function () {
	var a = 10;
	var b = 20;
	console.log(a + b); // 30
})();

console.log(a); // undefined
```

위와 같은 특이한 코드는 익명 함수를 만들고 즉시 실행하게 하는 코드이다.  
위 코드를 길게 풀면 다음처럼 쓸 수 있다.

```js
var tempFunction = (function() {
	var a = 10;
	var b = 20;
	console.log(a + b); // 30
});
tempFunction();
```
변수에 할당해서 재실행하지 않고, 즉각적으로 함수를 바로 실행한 것이라 볼 수 있는데요,  
변수나 함수를 외부에서 접근하지 못하게 숨기거나 충돌을 방지하기 위해 많이 사용되는 기법이다.

즉시 실행 함수에서 긴 변수를 호출 인자로 넘기고 파라미터를 짧게 쓴다면 다음처럼 코드를 줄이는 효과도 낼 수 있다.

```js
(function (b) {
	b.getElementById('content');
	...

})(document.body);

```

<hr>