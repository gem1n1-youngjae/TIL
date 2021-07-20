# CSS
## CSS 란?
> Cascading Style Sheets

`CSS`는 `HTML`을 웹 사이트에서 화면에 표시되는 정보를 약속 한 것 이다.
`CSS`는 구체적으로 어떤 스타일로 요소가 표시 되는지를 정하는 규격이라고 할 수 있다.

초기의 웹은 `HTM`L 하나로 문서의 뼈대도 만들고 꾸미기도 함께 하였지만,
공통적인 디자인을 갖는 문서가 여럿 존재 할 경우 하나의 디자인이 변경되면 모든 파일을 수정해야 하는 등의 번거로움이 존재했다.

`CSS`는 이런 문제를 해결함과 동시 웹페이지의 내용과 스타일(표현)을 분리해주며, 역할 분담도 되는 효과를 가지고 있다.

## 사용법
`CSS` 내부적으로 사용되는 문법은 동일하다. 그러나 어디에 기술하느냐의 차이가 존재한다.
`CSS` 를 사용하는 방법에는 3가지가 있다.

1. HTML 태그의 style 속성을 이용
2. `<style>` 태그를 통해 HTML 문서 내부에 기술 (<head> 태그 내부에 사용함 )
3. .css 파일로 분리하여 HTML 문서에 연결


###  HTML 태그의 style 속성을 이용
```html
<div style="color: red"> this is red text </div>
```
### `<style>` 태그를 통해 HTML 문서 내부에 기술
```html

<html>
<head>
	<style type="text/css">
		.my-text{ color: blue }
	</style>
</head>
<body>
	<div class="my-text">
		this is red blue
	</div>
</body>
</html>
```
> 1번 처럼 사용시 `HTML`과 `CSS`를 분리하는 장점이 없어지기 때문에 2,3번을 주로 활용한다.
 `<style>` 태그의 `type="text/css"`는 필수가 아니지만, 더 정확한 표현을 위해 함께 써준다.

### .css 파일로 분리하여 HTML 문서에 연결

`CSS`를 별도의 파일로 저장 후 HTML 문서 내에서 불러올 수 있다.

여러 웹페이지에서 공통적인 `CSS`를 참조할 때, 중복 코드를 제거할 수 있기에 매우 유용하며, 문서 규격과 스타일의 분리를 위해 `CSS`를 별도의 파일로 분리하여 사용하는 것이 좋다.

```html
<head>
	<link rel="stylesheet" href="경로.css" type="text/css">
</head>
```

#### 특별한 점
`CSS`의 인코딩은 문서 맨 앞에 `@charset "utf-8";` 형식의 코드를 쓰며 지정한다.
`CSS`에서 `background-image` 등으로 외부 파일을 참조할 때에는 웹페이지의 `url`이 아닌 `CSS` 파일의 경로를 기준으로 한다.

#### CSS 파일 예제
```css
@charset "utf-8";
/* 주석 */
/* @charset "utf-8"; 은 선택사항 */

text{
	font-size: 24px;
	font-weight: bold;
}

#login-btn{
	width: 99px;
	height: 45px;
	background-color: #ffffff;
}

.input_box{
	padding: 4px 6px;
	border-radius: 10px;
	text-decoration: none;
	background-color: #000000;
	color: #ffffff;
}
```