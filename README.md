# 허도경(HEO DO KYUNG) 마크업 가이드

본 마트업 가이드는 프로젝트를 협업/개인으로 진행시 통일된 코드를 유지하여 운영 및 코드의 재사용, 일관된 코드의 활용을 통해 보다 효율적이고 간결한 코드가 유지되게 하는것에 목적을 두고 있습니다.
해당 가이드는 [Code Guide by @mdo](http://mdo.github.io/code-guide)를 기반으로 작성하였으며 프로젝트를 진행하면서 느꼈던 부분과 개선이 필요하다고 생각한 부분을 첨부,첨삭 하였습니다.

- - -

1. [기본 규칙](#basic)
  - **[1.1 ID / Class 기본 규칙](#name-syntax)**
2. [들여쓰기 및 환경 설정](#editor)
3. [HTML](#html)
  - [3-1. Syntax](#html-syntax)
  - [3-2. Doctype](#html-doctype)
  - [3-3. 언어(lang) 속성](#html-lang)
  - [3-4. Metadata](#html-metadata)
  - [3-5. Elements](#html-elements)
  - [3-6. Attributes](#html-attributes)
4. [CSS](#css)
  - [4-1. CSS 문법](#css-syntax)
  - [4-2. 속성(property) 선언 순서](#css-property-order)
  - [4-3. 미디어 쿼리 위치](#css-media-query)
  - [4-4. 전처리문 계산식](#css-preprocessor-calculation)
  - [4-5. 주석](#css-comment)
  - [4-6. 네이밍 규칙](#css-naming)
  - [4-7. 선택자](#css-selector)
  - [4-8. 컴포넌트](#css-component)

- - -

## 1. 기본 규칙 <a id="basic" href="#basic">#</a>

W3C 문법과 레진 마크업 가이드라인을 지켜 코드를 작성합니다. 많은 사람이 참여했더라도 한명이 쓴 것처럼 보이는 코드가 좋습니다. 팀원들과 논의하여 업데이트할 수 있습니다.

### 1.1 ID / Class 기본 규칙 <a id="name-syntax" href="#name-syntax">#</a>
* 모든 엘리먼트 명과 애트리뷰트 명은 케밥 표기법(`kebab-case`) 작성을 원칙으로 합니다.
    * CSS의 모든 속성 역시 케밥 표기법으로 표기되고 가독성 및 오타방지, Shift의 사용없이 빠른 입력이 가능합니다.
* 재 사용성이 없는 ID는 사용하지 않고 Class로만 작성하며 레이아웃 역시 포함됩니다. (예: `<div class="header" />`, `<div class="footer" />`, `<div class="container" />`, `<div class="gnb" />` 등)

```html
<!-- Bad -->
<span class="searchForm"></span>
<span class="search_form"></span>

<!-- Good -->
<span class="search-form"></span>
```

- - -

## 2. 들여쓰기 및 환경 설정 <a id="editor" href="#editor">#</a>
규칙을 준수하기 위해 에디터 환경을 설정해 둡니다.

* 마크업의 중첩이 깊어질때마다 자식 엘리먼트의 들여쓰기는 1탭씩 들여쓰고, 1탭의 들여쓰기 공백문자는 4칸으로 합니다.
* 파일 저장 시 줄 끝 공백문자를 제거합니다.
* 파일 저장 시 UTF-8 인코딩으로 저장합니다.

- - -

## 3. HTML <a id="html" href="#html">#</a>

### 3-1. HTML 문법 <a id="html-syntax" href="#html-syntax">#</a>

* 들여쓰기는 공백문자 4 개를 사용합니다.
* 모든 애트리뷰트 값은 큰 큰 따옴표(")를 사용합니다.
* 단일 태그에는 슬래시(`/`)를 사용하지 않습니다. (예: `<br />`, `<img />`)
* 닫는 태그가 선택적이라도 생략하지 않습니다. (예: `</li>`, `</body>`)

```html
<!-- Bad -->
<input />
<br />

<!-- Good -->
<input>
<br>
```

### 3-2. HTML5 doctype <a id="html-doctype" href="#html-doctype">#</a>
모든 HTML 페이지 시작 지점에 공백 없이 HTML5 문서 타입을 선언합니다.
```html
<!DOCTYPE html>
<html>
    ...
</html>
```

### 3-3. 언어(lang) 속성 <a id="html-lang" href="#html-lang">#</a>
문서 루트인 `html` 요소에 `lang` 속성을 추가합니다.
* 영어: `en`
* 한국어: `ko`

```html
<html lang="ko">
```

### 3-4. Metadata <a id="html-metadata" href="#html-metadata">#</a>
`<head>` 엘리먼트의 자식 엘리먼트는 아래의 순서에 맞추어 선언합니다.

* Charset
* X-UA-Compatible
* Viewport
* Title
* Meta
* Style
* JavaScript

```html
<meta charset="utf-8">
<meta http-equiv="X-UA-Compatible" content="ie=edge">
<meta name="viewport" content="width=device-width,initial-scale=1.0,maximum-scale=1.0,minimum-scale=1.0,user-scalable=no,target-densitydpi=medium-dpi,viewport-fit=cover">
<title>페이지 타이틀 | Menu Depth level 2 | Menu Depth level 1</title>
<meta property="og:title" content="Hello, World!" />
<link rel="stylesheet" href="ui-common.css">
<script src="bar.js"></script>
```

#### A. Charset
문서의 기본 언어셋은 `UTF-8`으로 선언합니다.

```html
<meta charset="utf-8">
```

#### B. X-UA-Compatible
인터넷 익스플로러가 최신 버전의 IE로 화면을 렌더링하기 위하여 문서모드를 `Edge`로 사용합니다.

```html
<meta http-equiv="X-UA-Compatible" content="IE=Edge">
```

#### C. Title
페이지 타이틀은 가장 하위 뎁스의 페이지 타이틀을 기준으로 상위 뎁스까지 역순으로 작성하며 각 메뉴 타이틀은 Bar Pipe`( | )` 로 구분합니다.

```html
<title>페이지 타이틀 | Menu Depth level 2 | Menu Depth level 1</title>
```

#### D. Script
`<script>` 엘리먼트는 가급적 `<head>` 또는 `<body>` 엘리먼트의 가장 마지막에 작성을 원칙으로 합니다. 웹브라우저는 `<script>` 엘리먼트를 만나면 처리가 끝날 때까지 HTML 파싱을 멈춥니다.


### 3-5. Elements <a id="html-elements" href="#html-elements">#</a>

#### A. 마크업 간소화
모듈화를 고려하여 디자인적으로 반드시 필요한 마크업이 아닌 경우에는 불필요한 마크업은 간결하게 작성합니다.

```html
<!-- Bad -->
<div class="visual-wrap">
    <div><img src="..." alt="..."></div>
</div>

<!-- Good -->
<div class="visual-wrap">
    <img src="..." alt="...">
</div>
```

#### B. 스타일 제어가 어려운 엘리먼트
자식 엘리먼트 태그가 한정적이거나(ex. `<table>`) 스타일 제어에 한계를 가진 엘리먼트(ex. `<select>`)가 컴포넌트의 루트 역할로 쓰일 땐 나중에 발생할 유지보수를 고려해 `<div>`나 `<span>` 엘리먼트로 감싸는 것을 권장합니다.

> 이 외의 불필요한 엘리먼트 상속은 반드시 피해야 합니다!

```html
<!-- Not Bad -->
<table class="table"></table>
<select class="combobox"></select>

<!-- Good -->
<div class="table">
  <table></table>
</div>
<span class="combobox">
  <select></select>
</span>
```

#### D. 입력 필드

회원가입 폼의 입력 필드처럼 너비, 높이가 유동적이라면 인라인 스타일로 제어하세요. 이렇게 하면 불필요한 클래스 생성을 막을 수 있습니다.

```html
<!-- Bad -->
<input type="text" class="input input--width-120">
<input type="text" class="input input--width-180">

<!-- Good -->
<input type="text" class="input" style="width:120px">
<input type="text" class="input" style="width:180px">
```

### 3-6. Attributes <a id="html-attributes" href="#html-attributes">#</a>

#### A. 선언 순서
Attributes는 가독성을 위해 아래 순서대로 작성합니다. 또한 순서를 통일하면 Element들의 위치가 비슷해지기 때문에 수정이 용이해집니다.
1. 선택자로 사용하는 `id`, `class` 속성은 가장 앞에 선언합니다.
2. `name` 속성은 class 속성 다음에 선언합니다.
3. 콘텐츠를 설명하는 `alt`, `title`, `role`, `aria-*` 속성은 가장 뒤에 선언합니다.
4. 인라인으로 스타일 속성을 선언할 경우 가장 마지막에 선언합니다.

```html
<input class="input" type="text" id="user-id" name="UserId" title="아이디" style="width:100px">
<input class="form-control" type="text">
<img src="..." alt="..." title="...">
```

#### B. Boolean 애트리뷰트
HTML5에서는 Boolean 애트리뷰트를 선언하는 것 만으로도 `true` 속성값과 같기 때문에 반드시 필요한 상황이 아니라면 따로 값을 작성하지 않습니다.

```html
<!-- Bad -->
<button disabled="true"></button>

<!-- Good -->
<button disabled></button>
<option value="1" selected>1</option>
```

- - -

## CSS <a id="css" href="#css">#</a>
CSS와 SASS 등의 CSS 전처리기(CSS Preprocessor) 코드의 작성 규칙을 설명합니다.

### CSS 문법 <a id="css-syntax" href="#css-syntax">#</a>

* 들여쓰기는 사용하지 않습니다.
* 프로퍼티는 영문 소문자로 작성하세요.
* 일반적으로 쌍 따옴표(`""`)를 사용합니다. 단 background 이미지에는 따옴표를 생략합니다.
* selector와 여는 중괄호(`{`) 앞에는 가독성을 위해 항상 공백 하나를 포함합니다.
* 속성과 속성 사이에는 가독성을 위해 공백을 1개 사용하며 마지막은 항상 세미콜론(`;`)으로 끝냅니다.
* 문서의 언어셋은 `UTF-8`으로 최상위에 선언하세요. 언어셋이 정해진 번들링 파일이라면 선언하지 않습니다.

```css
.selector {property:value; property:value;}
```

선택자를 그룹핑하는 경우 쉼표(`,`) 뒤에서 줄바꿈합니다.
```css
/* X */
.selector1, .selector2 { ... }

/* O */
.selector1,
.selector2 { ... }
```

속성값에는 큰 따옴표(`""`)를 사용합니다.
```css
/* X */
[type=text] { ... }
[type='text'] { ... }
{ background: url('test.png'); }
{ background: url("ex.png"); }

/* O: 속성 선택자 속성값에 쌍 따옴표 사용 */
[type="text"] { ... }
{ background: url(test.png); }
```

괄호(`()`) 안에서는 쉼표(`,`) 뒤에 공백을 넣지 않습니다.
```css
/* X */
    color: rgba(0, 0, 0, .5);

/* O */
    color: rgba(0,0,0,.5);
```

축약 가능한 값을 축약합니다.
```css
/* X */
    color: #ffffff;
    font-weight: normal;
    font-weight: bold;
    border: none;
    opacity: 0.5;
    border-width: 0px;
    background-size: 100% auto;
    background-position: 50% 50%;

/* O */
    color: #fff;
    font-weight: 400;
    font-weight: 700;
    border: 0;
    opacity: .5;
    border-width: 0;
    background-size: 100%;
    background-position: 50%;
```

의미있는 블럭 기준으로 빈 줄을 포함합니다.
```css
/* 의미있는 블럭 기준으로 빈 줄 포함 */
/* 헤더 */
.header { ... }
.header__element { ... }

/* 풋터 */
.footer { ... }
.footer__element { ... }
```


### 속성(property) 선언 순서 <a id="css-property-order" href="#css-property-order">#</a>
박스모델 관련 속성을 가장 먼저 작성하고 그 뒤 포지셔닝 속성을 선언한 후 나머지는 뒤에 놓습니다. 추후 수정이 발생했을 때 용이하게 하기 위해 Background 속성은 가장 마지막에 선언합니다.
```css
{
/* Box-model */
    display:block;
    float:right;
    width:100px;
    height:100px;
    padding:20px;
    margin:10px;
/* Positioning */
    position:absolute;
    top:0;
    right:0;
    bottom:0;
    left:0;
    z-index:100;
/* Typography */
    font:normal 13px "Helvetica Neue", sans-serif;
    line-height:1.5;
    color:#333;
    text-align:center;
/* Border */
    border:1px solid #e5e5e5;
    border-radius: 3px;
/* etc */
    opacity:1;
/* Background */
    background-color:#f5f5f5;
}
```

### 미디어 쿼리 위치 <a id="css-media-query" href="#css-media-query">#</a>
미디어쿼리는 컴포넌트 단위로 분류하여 관련 규칙 바로 뒤에 작성합니다. 파편화된 스타일이 한곳으로 모여져 가독성을 높입니다.

```css
.element { ... }
.element-avatar { ... }
.element-selected { ... }
@media (min-width: 640px) {
    .element { ... }
    .element-avatar { ... }
    .element-selected { ... }
}
```


### 전처리문 계산식 <a id="css-preprocessor-calculation" href="#css-preprocessor-calculation">#</a>
계산식에 괄호를 사용합니다.
```css
/* Bad example */
.element { margin: 10px 0 @variable*2 10px; }

/* Good example */
.element { margin: 10px 0 (@variable * 2) 10px; }
```

### 주석 <a id="css-comment" href="#css-comment">#</a>
주석은 간결하게 작성합니다. scss 파일은 한 줄 주석(`//`) 사용이 가능하지만 CSS 파일에 남지 않습니다.
```css
/* Bad example */
/* Modal - Wrapping element for .modal-header, .modal-body, modal-footer  */
.modal {
    ...
}

/* Good example */
/* Modal */
.modal {
    ...
}
```

### 네이밍 규칙 <a id="css-naming" href="#css-naming">#</a>

> 이 규칙은 *<a target="_blank" href="https://en.bem.info/methodology/naming-convention/">BEM</a>* 을 기반으로 작성되었습니다.

* 클래스 이름 규칙은 [BEM(Block Element Modifier)](http://getbem.com/naming/)스타일을 따릅니다.
* 스타일 제어를 위해 아이디 선택자의 사용을 하지 않습니다.
* 클래스 이름은 명은 케밥 표기법(`kebab-case`) 작성을 원칙으로 하며 숫자, 더블 대시(`--`), 더블 언더스코어(`__`)만 사용합니다.
* 짧고 간결하게 작성하되 축약하지 않습니다. `.btn`과 같이 쉽게 의미를 유추 할 수 있는 축약은 괜찮지만 `.bn`와 같이 의미를 파악하기 어려운 축약은 사용하지 않습니다.
  **클래스명은 페이지에 상속받지 않으며, 디자인(시각적 표현)보다는 구조, 기능, 목적을 나타내는 이름으로 네이밍 합니다.**
  **클래스명은 반드시 엘리먼트의 의미를 전부 담아서 네이밍 합니다.**
* 변화 또는 상태를 나타내는 추가 클래스는 블록 또는 요소 이름에 더블 대시(`--`)를 붙여 작명합니다.


#### A. Naming

Syntax: `<BLOCK>[__<ELEMENT>][--<MODIFIER>][.is|has-<STATE>]`

- 기본 네이밍 규칙은 BEM을 따릅니다.
  ```BLOCK__ELEMENT--MODIFIER```
- 상태 클래스는 `modifier`에서 분리하여 따로 관리합니다.
  ```BLOCK__ELEMENT--MODIFIER.is-STATE```

```html
<div class="widget">
  <div class="widget__wrapper widget__wrapper--dark">
    <input class="input" type="text" aria-label="Text Field">
    <button class="btn" type="reset">Reset</button>
    <button class="btn btn--submit is-disabled" type="submit" disabled>Submit</button>
  </div>
</div>
```

```css
/* Bad */
.sform { ... }
.themeLezhin { ... }
.sf-input { ... }
.sf-btn { ... }
.SearchformButtonDisabled { ... }

/* Good */
.widget {} /* BLOCK */
.widget__wrapper {} /* BLOCK__ELEMENT */
.widget__wrapper--dark {} /* BLOCK__ELEMENT--MODIFIER */
.input {} /* BLOCK */
.btn {} /* BLOCK */
.btn.is-disabled {} /* .BLOCK.is-STATE */
.btn--submit {} /* .BLOCK--MODIFIER */
.btn--submit.is-disabled {} /* .BLOCK--MODIFIER.is-STATE */
```

### 선택자 <a id="css-selector" href="#css-selector">#</a>
* 타입 선택자를 사용하지 않습니다. 클래스 선택자를 사용합니다.
* 선택자 우선순위(specificity)를 높이는 조합과 중첩을 사용하지 않습니다. 조합과 중첩은 3회를 초과하지 않습니다.
* 여러 클래스를 묶을 때 쉼표 후 개행합니다.

```css
/* Bad example */
section.tweet > header { ... }
section.tweet > header.tweet__header { ... }
.tweet > .tweet__header, .tweet > .tweet__username { ... }

/* Good example */
.tweet { ... }
.tweet__header,
.tweet__username { ... }
```

### 컴포넌트 <a id="css-component" href="#css-component">#</a>
* 컴포넌트 별로 코드를 모아서 작성합니다.
* 계층 구조의 순서에 따라 작성합니다.
* 코드 블럭을 분리할 때 공백(줄 바꿈)을 일관성 있게 사용합니다.
* 여러개의 *.scss 파일을 나눌 때, 페이지보다는 컴포넌트 별로 나눕니다.

```css
/* Modal: modal.scss */
.modal { ... }
.modal__header { ... }
.modal__body { ... }
.modal__footer { ... }
.modal__footer--disabled { ... }
```

- - -

