### BOM vs DOM

---

- 브라우저를 통해 우리는 컨텐츠를 볼 수 있고, 필요한 정보를 얻음

- 프론트엔드 개발자는 사용자들이 브라우저 내에서 인터렉션을 할 수 있도록 DOM과 다양한 이벤트들을 사용함

- DOM API : 화면 요소에 접근

- BOM API : 브라우저 정보 제공

<div style="margin: 50px"></div>

### DOM (Document Object Model : 문서 객체 모델)

---

- HTML, XHTML 문서용 API

- 사용자와 브라우저 간의 인터페이스 역할을 하며, 해당 요소를 나타내는 노드와 노드의 속성을 나타내는 프로퍼티, 그리고 프로퍼티들을 조작할 수 있는 메서드가 담긴 구조화된 객체

- DOM을 이용해서 자바스크립트 언어로 특정 요소에 접근해 구조나 내용, 스타일 등등을 변경 가능

- DOM 없이는 자바스크립트가 우리가 보는 웹 사이트에 대한 정보를 알 수 없음

- DOM API는 Document를 통해 사용 -> DOM 트리의 진입점 & 브라우저가 불러온 웹 페이지 = Document 인터페이스

<div style="margin: 50px"></div>

### DOM 트리 (DOM Tree)

---

- DOM은 문서를 노드의 계층적 트리 구조로 나타냄

- 노드는 다른 노드와의 관계가 있을 수 있고, 서로 다른 특징, 데이터, 메서드를 가짐

- 노드와 노드 사이의 관계가 트리 노드로 표현되는 것

- 트리의 최상위 노드는 root라고 하고 HTML 문서에서는 일반적으로 `<html>`이 root 노드라고 볼 수 있음

  ```html
  <!DOCTYPE html>
  <html>
    <head>
      <title>DOM</title>
    </head>
    <body>
      <h1 id="title">DOM Tree</h1>
      <!-- 이 부분은 주석 -->
    </body>
  </html>
  ```

  ```
  // 단순화한 DOM Tree

  Document
    -> HTML
        -> HEAD
            -> TITLE
                -> (#text) DOM
    -> BODY
        -> H1
            -> Attribute(id)
                -> (#text) title
            -> (#text) DOM Tree
        -> (#comment) 이 부분은 주석
  ```

  - 트리의 시작은 Document이며, 노드가 가진 타입에 따라 Element, Text, Attr 타입으로 분류되어 구조를 가짐

  - Text 노드는 각 트리 노드의 리프노드가 됨

  - 주석은 화면에 나타나지 않지만, DOM 트리에 포함됌

<div style="margin: 50px"></div>

### 노드 (Node)

---

- 노드 인터페이스는 객체 형태로, 문서의 요소들에 대한 기본 데이터 타입을 의미

- 즉, DOM 트리의 구성 요소이며, nodeType, nodeName, nodeValue, 자식 노드 & 형제 노드에 대한 관계 등등의 정보를 가짐

  - nodeType : 12개의 노드 타입을 정수로 나타냄

  - nodeName : 노드의 이름

  - nodeValue : 노드의 값

- 노드 조작 메서드를 사용할 수 있음 (ex. appendChild)

- 노드의 계층 구조 (트리 형태)

  ```
  // > : 왼쪽을 상속받은 오른쪽

  EventTarget (이벤트가 발생했을 때 이벤트의 대상)
    > Node
      > Text
      > Comment
      > Element
        > HTML Element
          > HTML Body Element
          > HTML Input Element
          > HTML Button Element
          > ...
  ```

  - Node : EventTarget을 상속 받음, DOM 노드의 기초, DOM 노드 관계를 나타내는 기능들이 포함됨

  - Element : Node를 상속 받음, DOM 요소 생성에 기본, 요소 탐색 및 이벤트 리스너 등 여러 메서드 제공

  - HTML Element : Element를 상속 받음, HTML 요소 구현

  - 상속 여부는 `instanceof`를 통해 확인

- DOM 프로퍼티에 접근하고 싶을 때는 객체 접근 방식과 동일하게 접근 가능 (점, 괄호 표기법 활용)

- 객체처럼 접근이 가능하다보니, 미리 정의된 프로퍼티가 아닌 새로운 프로퍼티를 정의해 사용할 수 있지만, 지양하는 방법임

- DOM 트리에서 최상위 노드를 제외하고는 모두 각각 하나의 부모 노드를 가지고, 여러개의 자식을 가질 수 있음 (자식들간의 관계는 형제 관계로 불림)

- DOM 트리에서의 계층 관계에 대해 노드에서 제공하는 프로퍼티들
  | property | 의미|
  |---|---|
  |parentNode | 부모 노드 반환|
  |childNodes | 자식 요소 반환 (NodeList)
  | firstChild | 첫번째 자식 반환 (없으면 null)|
  | lastChild | 마지막 자식 반환 (없으면 null)
  | nextSibiling | 부모의 자식 노드 중 자신의 다음에 있는 노드 반환 (없으면 null)
  | previousSibiling | 부모의 자식 노드 중 자신의 이전에 있는 노드 반환 (없으면 null)

- DOM 트리 전체 노드 순회

  ```js
  // childNodes 프로퍼티는 배열 반환
  document.body.childNodes.forEach((node) => {
    console.log(node);
  });
  ```
