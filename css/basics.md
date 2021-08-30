# CSS (Cascading Style Sheets)

스타일, 레이아웃 등을 통해 문서(HTML)를 표시하는 방법을 지정하는 언어

<br>

### CSS 구문

```css
/* CSS 구문은 선택자(h1)와 함께 열린다. */
/* 선택자를 통해 스타일을 지정할 HTML 요소를 선택한다. */
h1 {
    
    /* 중괄호 안에서는 하나의 쌍 (속성: 값;)으로 이루어진 선언을 진행 */
    /* 속성 = 어떤 스타일 기능을 변경할 지 결정 */
    /* 값 = 어떻게 스타일 기능을 변경할 지 결정 */
    color: blue;
    font-size: 15px;
}
```

### CSS 정의 방법

* 인라인(inline) : 해당 태그에 직접 `style` 속성을 활용

* 내부 참조(embedding) : `<head>` 태그 내에 `<style>`을 지정

* 외부 참조(link file) : 분리된 CSS 파일을 `<head>` 내의 `<link>`를 통해 불러옴

  ```css
  <link href="주소/파일명.css" rel="stylesheet">
  ```

<br>

## CSS Selectors

HTML 문서에서 특정 요소를 선택하여 스타일링 하기 위해, 선택자라는 개념이 필요

### 기본 선택자

* 전체 선택자, 요소  선택자
* 클래스 선택자, 아이디 선택자, 속성 선택자

### 결합자(Combinators)

* 자손 결합자, 자식 결합자
* 일반 형제 결합자, 인접 형제 결합자

```css
<style>
	* {} 		: 전체 선택자
	h2 {} 		: 요소 선택자
	.green {} 	: 클래스 선택자
	# purple {} : id 선택자
	.box > p {} : 자식 결합자 - 바로 아래(깊이) 요소들
	.box p {} 	: 자손 결합자 - 하위의 모든 요소들
	div ~ p {}	: 일반 형제 결합자 - 뒤에 위치하는 형제 요소들
	div + p {}	: 인접 형제 결합자 - 바로 뒤에 위치하는 형제 요소
</style>
```

### CSS 적용 우선순위 (Cascading order)

```css
!important > 인라인 > id 선택자 > class 선택자 > 요소 선택자 > 소스 순서
```

### CSS 상속

부모요소의 속성 중 Text 관련 요소는 상속 O, Box model 관련 요소나 position 관련 요소는 상속 X.

<br>

## CSS 단위

### 크기 단위

px(픽셀), %(백분위), em(바로 위 부모요소의 상대비), rem(최상위요소인 html의 상대비), viewpoint(화면)

### 색상 단위

색상키워드(특정 색), RGB(16진수나 함수형), HSL(함수형)

<br>

## Box model

모든 HTML 요소는 box 형태로 되어있으며, 하나의 박스는 Margin, Border, Padding, Content의 네 부분으로 이루어진다.

### Box-sizing

* 기본적으로 모든 요소의 box-sizing은 content-box (순수 content 영역만을 box로 지정)
* box-sizing을 border-box로 바꾸면 border까지의 영역으로 볼 수 있다.

<br>

## CSS Display

HTML 요소들을 시각적으로 어떻게 보여줄지 결정하는 속성

### display: block

* 줄 바꿈이 일어나며, 화면 크기 전체 가로폭을 차지한다.
* 블록 레벨 요소 안에 인라인 레벨 요소가 들어갈 수 있다.
* ex. div / ul, ol, li / p / hr / form 등

### display: inline

* 줄 바꿈이 안 일어나며, content 너비만큼 가로폭을 차지하기 때문에 width, height, margin을 지정할 수 없다.
* 상하 여백은 line-height로 지정한다.
* span / a / img / input, label / b, em, i, strong 등

### display: inline-block

* inline처럼 한 줄에 표시 가능하며, 
* block 처럼 width, height, margin 속성을 모두 지정할 수 있다.

### display: none

* 해당 요소를 화면에 표시하지 않고 공간조차 사라진다.
* cf. visibility: hidden 은 해당 요소가 공간은 차지하나 화면에 표시만 하지 않는다.

<br>

## CSS Position

문서상에서 요소를 배치하는 방법을 지정

### static : 기본 위치

* 부모 요소 내에서 배치될 때는 부모 요소의 위치를 기준으로 배치

### relative : 상대 위치

* 자신의 static 위치를 기준으로 이동
* 원래 있던 위치도 계속 차지함

### absolute : 절대 위치

* 원래 있던 위치는 비워줌
* static이 아닌 가장 가까운 부모/조상 요소를 기준으로 이동 (없으면 body)

### fixed : 고정 위치

* 원래 있던 위치는 비워줌
* viewpoint를 기준으로 이동
* 스크롤 시에도 항상 같은 곳에 위치
