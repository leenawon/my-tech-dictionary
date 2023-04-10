### DOM 이벤트 (Event)

---

- 이벤트 객체

  - DOM에서 발생한 이벤트에 대한 정보를 담은 객체

  - 이벤트의 종류, 요소 정보, 캡쳐링 여부, 이벤트 발생 위치 등등...

  - target vs currentTarget : 이벤트가 발생한 요소에 접근할 때 사용 (같은 값 or 다른 값)

    | 종류          | 값                                          |
    | ------------- | ------------------------------------------- |
    | target        | 처음 이벤트가 발생했던 대상 (DOM 요소) 참조 |
    | currentTarget | 발생한 이벤트가 등록된 대상 (DOM 요소) 참조 |

- stopPropagation() vs preventDefault() : 이벤트 제어 메서드

  - preventDefault()

    - 이벤트를 취소할 수 있는 경우, 이벤트 취소

    - 전파되는 이벤트는 막지 않음 (캡쳐링, 버블링)

    - 단지 현재 이벤트의 기본 동작만 중단

  - stopPropagation()

    - 기본 동작 중지는 못함

    - 전파되는 이벤트를 막음 (캡쳐링, 버블링)

- addEventListner

  - 이벤트 타입에 여러 가지의 리스너 등록 가능

  - 버블링 또는 캡쳐링 사용 여부 등의 제어 가능

    ```js
    document.getElementById("container").addEventListner(
      "click",
      (e) => {
        console.log(e);
      },
      true
    ); // 캡쳐링 사용 여부 : true
    ```

- removeEventListner

  - 할당한 이벤트 제거

  - 제거하고 싶은 이벤트 리스너의 참조를 인자로 넘겨줌 (반드시 동일한 참조를 가진 리스너를 넘겨줄 것!)

    ```js
    const container = document.getElementById("container");

    function listner() {
      console.log("listner");
    }

    container.addEventListner("click", listner);
    container.removeEventListner("click", listner); // 동일하게 작성
    ```

- 버블링 vs 캡쳐링

  - 계층적인 구조를 가진 DOM 요소에 이벤트가 발생하면 이벤트가 전파되는 현상

    ```html
    <!-- section, div, span 요소 모두 addEventListner를 이용해 이벤트를 등록해놓은 상태라고 가정 -->
    <section>
      <div>
        <span></span>
      </div>
    </section>
    ```

  - **버블링** : 이벤트 발생 후 부모 (상위) 요소 방향으로 전파되는 현상 (대부분의 이벤트들이 갖는 흐름)

    `<span> 요소 (클릭) ->  <div> 요소 -> <section> 요소`

  - **캡쳐링** : 이벤트가 발생하면 상위 부터 시작해서 자식 (하위) 요소 방향으로 전파되는 현상 (addEventListner의 세 번째 옵션으로 설정 가능)

    `<section> 요소 -> <div> 요소 -> <span> 요소 (클릭)`

  - 두 가지가 동시에 있는 경우? : 캡쳐링 이후 버블링

    `<section> 요소 캡쳐링 -> <div> 요소 캡쳐링 -> <span> 요소 (클릭) 캡쳐링 -> <span> 요소 (클릭) 버블링 -> <div> 요소 버블링 -> <section> 요소 버블링`

- 이벤트 위임

  - 이벤트 버블링 현상을 이용해 이벤트 발생을 제어하는 패턴 (버블링일 때만 가능)

  - 이벤트 제어를 진짜 타겟의 상위 요소로 위임

  ```html
  <div id="button-container">
    <button></button>
    <button></button>
    <button></button>
    <button></button>
    <button></button>
    <!-- ..... 500개 -->
  </div>
  ```

  - 예시 상황 : div 태그 안에 500개의 button 태그가 있다고 가정했을 때, button 별로 이벤트 리스너를 만들기에는 500개를 만들어야 하는 상황 발생

  - 이런 상황에서는 불필요하게 반복되는 코드를 초래하기 때문에 이벤트 위임을 이용하는 것이 간결하게 작성 할 수 있는 방법!

  ```js
  const container = document.getElementById("button-container");

  container.addEventListner("click", (e) => {
    console.log(e);
  });
  ```

  - button 태그에 하나하나 이벤트를 달아줄 필요 없이, 부모 태그에 이벤트를 달고 이벤트 버블링 현상을 이용하면, button 태그를 클릭 했을 때, 부모 요소인 div의 이벤트가 동작하게 되는 것!

  - 장점 : 부모 속에 많은 자식 요소들의 이벤트를 제어해야하는 경우나, DOM에 동적으로 추가되는 요소가 있을 때 효율적

  - 단점 : 이벤트의 진짜 타겟을 기준으로 이벤트를 정의하는 것이 아니므로 이벤트가 어떻게 동작할지 파악하는데 있어서 가독성이 떨어짐
