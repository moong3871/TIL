**처음: 따라만들어보고 실제 페이지 분석해보면서 흥미를 잃지 않기**

> Web과 HTML

- W3C - HTML5 / WHATWG - HTML Living Standard
- HTML: **Hyper Text Markup** Language --> 웹페이지 작성을 위한 (구조를 잡기 위한) 언어
  - Hyper Text: 한 문서에서 다른 문서로 즉시 이동
  - Markup: 역할 부여(제목이 제목)
  - Markup Language: 문자나 데이터의 구조 명시, '표현만'

> HTML 기본 구조

- html 요소: head와 body로 구분

  - head: 문서 정보를 담고 있다. 브라우저에 보이지는 않는다.

    - head에 들어가는 기술: open graph protocol (url보낼 때 미리보기 화면)

  - body: 브라우저 화면에 나타나는 실제 내용

    - DOM 트리

      부모 다음에 자식이 오면 **2spaces 혹은 4spaces**

> 요소

- 요소의 구성: 태그와 내용(contents), '<h1> contents <h1>' (여는 태그 닫는 태그)

- 속성: 태그별로 사용할 수 있는 속성은 다르다.

  `<a href="https://google.com"></a>`

  **href 뒤에 공백은 NO!, 쌍따옴표 사용!**



크롬 개발자 도구 켜기: ctrl shift I 또는 오른쪽마우스-검사 또는 F12

> **시맨틱 태그**

:의미있는 태그 ex) header, nav, asdie 등이 시맨틱 태그 / div는 시맨틱 태그 아님

`<div>`적힌 것보다 `<head>`적혀 있으면 아 이게 head구나 하고 알기 쉽다.

장점

1. 읽기가 쉬워진다.(개발자)

   - 개발자가 의도한 요소의 의미가 명확히 드러남.

   - 코드의 가독성을 높이고 유지보수를 쉽게 함.

2. 접근성이 좋아진다.

   - 검색엔진 -> 시력장애용 스크린리더 -> 더 나은 사용자 경험을 제공



> 블럭/인라인

:블럭은 다음 요소가 아래에, 인라인은 옆에 올 수 있다.

> 텍스트 관련 요소

`<a>`: 하이퍼링크 생성

`<b> 랑 <strong>`: 글자를 굵게, b는 그냥 굵게, strong은 굵게 + 강조

`<i> 랑 <em>`: 이탤릭체, i는 그냥 이탤릭, em은 이탤릭+강조

> **form**

사용자의 입력을 받아서 서버로 보내주는 역할

검색창이 form tag로 구성돼있음

- form 의 기본 속성
  - action
  - method: get, post
- input
  - form tag안에는 input tag가 존재

# CSS

스타일과 레이아웃을 통해 사용자에게 어떻게 진행되는지

> CSS 구문

`선택자` h1 로 구문 시작, `선언은 속성과 값으로 구성` 

```
h1 {
	color:blue;
	front-size: 15px; 
}
```

> CSS 정의 방법

- 인라인

- 내부참조: style 안에 정의

- 외부참조: css 파일을 따로 만들어서 link 태그로 적용 (기본)

  

> CSS Selectors

- 네이버 F12 사전클릭 copy selector

#NM_FAVORITE > div.group_nav > ul.list_nav.NM_FAVORITE_LIST > li:nth-child(1) > a

> CSS 적용 우선순위

- 중요도: `!important` 덧붙일시 우선순위 1위
- 인라인 / id 선택자/ class선택자/ ... /요소 선택자
- 소스 순서

> CSS 상속

- 부모 요소의 속성을 모두(X) 자식에게 상속한다. 상속 되는 것도 있고 안 되는 것도 있다.

> CSS 단위

- (상대) 크기 단위: px, %, **em**, **rem**

  (em은 부모의 사이즈에 따라 자식이 결정, rem은 html 태그 사이즈와 비교하여 배수 단위)

- Viewport 기준 단위

> 색상 단위

- RGB 색상

- HSL색상은 채도 (a는 투명도)

> CSS 문서 표현

- 배경(background-image)은 컨텐츠와 관련없는 단순 디자인 요소
  - cf) img: 디자인+컨텐츠

> **CSS Box model**

- margin-border-padding-content

  - 축약형태 시 순서는 상관x

    - ```python
      #값 하나: 상하좌우
      margin-1{
      	margin: 10px;
      }
      #값 둘: 상하/ 좌우
      margin-2{
          margin:10px 20px;
      }
      #값 셋: 상/좌우/하
      margin-3{
          margin:10px 20px 30px;
      }
      #값 넷: 상우하좌(시계방향)
      margin-2{
          margin:10px 20px 30px 40px;
      }
      ```

- margin 상쇄

> CSS Display

- display inline은 **margin값을 줄 수 없다.** 상하 여백인 line-height로 지정
- text와 관련된 요소는 inline 요소
- block은 너비를 가질 수 없다면 오른쪽을 다 차지
- inline은 컨텐츠 영역만큼만 차지
- 정렬은 기본적으로 좌측부터, margin-left하면 왼쪽값을 오른쪽에 옮긴다.
- inline-block: block처럼 margin 지정 가능, inline처럼 한 줄에 표시 가능
- none: 화면에 표시하지 않고, **공간도 사라진다**.(만약 아래에 박스가 있었다면 위로 올라온다.)
  - visibility : hidden은 공간은 차지하지만 화면에 표시하지는 않는다.

> **CSS position**

- static/ relative/ absolute/ fixed
  - absolute는 **static이 아닌** 부모나 조상을 기준으로 움직임
  - fixed는 브라우저를 기준