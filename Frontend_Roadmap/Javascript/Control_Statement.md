## 제어문

### 조건문

#### if, else 문
```js
if (score >= 90)
	alert('A');
else if (score >= 80)
	alert('B');
else if (score >= 70)
	alert('C');
else
	alert('F');
```

#### switch 문
```js
switch (n) {
	case 0 :
	    // action 0
		break;

	case 1 :
	    // action 1
		break;
}
```

#### 비교 연산자

<table>
	<tr>
	    <td><code>a < b</code></td>
	    <td>a가 b보다 작다</td>
	</tr>
	<tr>
	    <td><code>a > b</code></td>
	    <td>a가 b보다 크다</td>
	</tr>
    <tr>
	    <td><code>a == b</code></td>
	    <td>a가 b보다 같다</td>
	</tr>
    <tr>
	    <td><code>a != b</code></td>
	    <td>a가 b보다 같지 않다</td>
	</tr>
    <tr>
	    <td><code>a >= b</code></td>
	    <td>a가 b보다 크거나 같다</td>
	</tr>
    <tr>
	    <td><code>a <= b</code></td>
	    <td>a가 b보다 작거나 같다</td>
	</tr>
</table>

#### 논리 연산자

<table>
	<tr>
	    <td><code>&&</code></td>
	    <td>AND 연산자</td>
	</tr>
	<tr>
	    <td><code>||</code></td>
	    <td>OR 연산자</td>
	</tr>
    <tr>
	    <td><code>!</code></td>
	    <td>NOT 연산자</td>
	</tr>
</table>

#### boolean
자바스크립트에서 비교 연산의 결과나 논리 연산은 0과 1이 아닌, `boolean` 타입으로 이루어집니다.
`boolean`타입에서는 `true`와 `false`가 존재하는데, 0을 `boolean`으로 형변환하면 `false`가 되고 1을 형변환하면 `true`가 되기 때문에 조건문 내부에 0이나 1을 넣어도 정상적으로 동작합니다.

몇 가지 값 이외에는 `boolean` 형변환시 모두 `true`가 됩니다.
`false`가 되는 특정한 값들은 아래가 있습니다.

- `0`
- `"" (빈 문자열)`
- `undefined`
- `null`
- `NaN`

<hr>

### 반복문

#### while문
```js
var i = 0;
while (true) {
	document.write(i);
	if (++i > 5) break;
}
```

#### for문
```js
var colors = ['red', 'blue', 'green'];
for (var i = 0; i < 3; i++) {
	document.write( colors[i] );
}
```

#### for in문
배열이나 객체의 경우, 내부 값을 간단한 방법으로 순회할 수 있다.

```js
var colors = ['red', 'blue', 'green'];
var me = {
	'name': 'young',
	'birth': 1996,
	'sex': 'm'
}

document.write('<h3>colors</h3>');

for (var i in colors){
    document.write( i + ': ' + colors[i] + '<br>' );
}

document.write('<h3>me</h3>');

for (var i in me){
    document.write( i + ': ' + me[i] + '<br>' );
}
	
```

**for in문 출력 결과**
```
colors
0: red
1: blue
2: green
me
name: young
birth: 1996
sex: m
```
<hr>