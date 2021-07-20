## HTML?

`Hyper Text Mark-up Language` 의 약자이다.
페이지에 제목, 문단, 표, 이미지, 동영상 등을 정의하고 그 구조와 의미를 부여하는 정적 언어로 웹의 구조를 담당한다.
**`프로그래밍 언어`가 아니다. `마크업 언어`이다.**

---

### HTML의 기본 형태

태그는 각자의 의미를 가지고 있다.

>

```html
<a></a>
<p>hello world</p>
```

태그는 열리고 닫히는 태그 구조로 구성 되어 있다.
태그는 `<>(꺾쇠 괄호)`로 둘러싸인 키워드이다.
닫히는 태그는 태그의 이름 앞에 `/(슬래시)`가 붙는다.

---

### 주석

HTML에도 주석이 있다.
주석은 코드를 이해하는데 도움을 주며, 당연히 웹 페이지에는 표시되지 않는다.

>

```HTML
<!-- 주석 -->
<!--
이런 식으로도 사용 가능 합니다.
-->
```

주석은 `<!--` 로 열리고 `-->` 로 닫히며, 사이에 설명을 적어으면 된다.

---

### 빈 태그 (empty tag)

HTML에는 닫히는 개념이 없는 태그들 존재한다.

>

```html
<!-- HTML4.01 방식 -->
<img />
<input />
<br />
<!-- XHTML1.0 방식 -->
<img />
<input />
<br />
```

`HTML5`에서는 두 가지 방식 모두 허용한다.

---

### 속성(Attributes)과 값(Value)

태그는 속성(attribute)과 값(Value)을 가질수 있다.

>

```html
<img src="./photo.jpg" alt="사진" />
<div class="name">유영재</div>
```

- `src(source)`라는 속성을 사용해서 삽입할 때 이미지의 경로를 지정했다.
- `alt(alternative)`라는 속성은 이미지를 출력하지 못하는 상황에 이미지 대신 보여질 텍스트를 지정했다.
- `div`태그에 `유영재`라는 텍스트를 넣었지만 무엇을 의미하는지 모르므로 `name`이라는 `class`을 추가했다.

---

### HTML의 부모와 자식 관계

태그A가 태그B의 콘텐츠로 사용되면, 태그B는 태그A의 부모 요소, 태그A는 태그B의 자식 요소라고 한다.

>

```html
<부모>
  <자식></자식>
</부모>
```

```html
<section class="drink">
  <h1>음료수</h1>
  <ul>
    <li>콜라</li>
    <li>사이다</li>
    <li>맥콜</li>
    <li>오렌지</li>
  </ul>
</section>
```

- `<section></section>`안에는 `<h1>`태그, `<ul>`태그, `<li>`태그가 있고, `<ul>`태그 안에는`<li>` 태그가 있다.
- `<section>`는 `<h1>`태그과 `<ul>`태그의 부모 요소이다.
- `<ul>`태그는 `<li>`태그의 부모 요소이다.
- `<h1>`태그과 `<ul>`태그는 `<section>`의 자식 요소이다.
- `<li>`태그는 `<ul>`태그의 자식 요소이다.
- `<section>`은 `<li>`태그의 조상(상위) 요소, 반대로 `<li>`태그는 `<section>`태그의 후손(하위) 요소이다.

## HTML 문서의 범위

> 예시 HTML 코드
>
> ```html
> <!DOCTYPE html>
> <html>
>   <head>
>     <meta charset="UTF-8" />
>     <meta name="author" content="유영재" />
>     <meta name="description" content="예시 HTML" />
>     <title>index</title>
>     <link rel="stylesheet" href="./css/style.css" />
>     <script src="./js/script.js"></script>
>   </head>
>   <body>
>     <section>
>       <h1></h1>
>       <div>
>         <ul>
>           <li></li>
>           <li></li>
>         </ul>
>       </div>
>     </section>
>   </body>
> </html>
> ```

### DOCTYPE(DTD, 버전 지정)

DOCTYPE(DTD, Document Type Definition)은 마크업 언어에서 문서 형식을 정의한다.
이는 웹 브라우저에 우리가 제공할 HTML 문서를 어떤 HTML 버전의 해석 방식으로 구조화하면 되는지를 알려준다. (HTML은 크게 1, 2, 3, 4, X-, 5 버전이 존재한다.)

> 현재의 표준 모드는 HTML5 이

### HTML(전체 범위)

`<html>`는 HTML 문서의 전체 범위를 지정한다.
웹 브라우저가 해석해야 할 HTML 문서가 어디에서 시작하며, 어디에서 끝나는지 알려주는 역할을 한다.

### BODY(구조 범위)

웹 브라우저가 해석해야 할 HTML 문서의 구조 범위를 지정한다.
구조는 사용자가 화면을 통해서 볼 수 있는 내용(콘텐츠)의 형태나 레이아웃 등을 의미하며 로고, 헤더, 푸터, 내비게이션, 메뉴, 버튼, 입력창, 팝업, 광고 등 보이는 모든 것들이 구조에 해당한다.
구조는 BODY 범위 안에서만 생성한다.

## HTML 태그 정리

<a href="https://heropy.blog/2019/05/26/html-elements/">한눈에 보는 HTML 요소(Elements & Attributes) 총정리 [heropyblog]<a>

<br>
<br>