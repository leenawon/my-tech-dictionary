### BOM (Browser Object Model)

---

- 웹 브라우저와 관련된 객체 모델

- DOM과의 차이점 : 표준이 없어 브라우저 별로 다르게 구현되어있음

- **window** 객체

  - 자바스크립트가 작동할 수 있도록 브라우저에서 제공하는 기능들은 window 객체를 통해 사용 가능

  - **브라우저 환경** => 자바스크립트 **전역 객체**를 의미

    - window 객체를 통해 전역 변수나 함수 접근 가능

  - **브라우저 창** 그 자체를 의미

    - 창 닫기, 새 창 띄우기, 경고 띄우기 등등,,,

    - 브라우저 속 각각의 탭들이 각각 하나하나의 window

- **History** 객체

  - 현재 탭/프레임 에서의 방문 기록 (현재 브라우저의 세션 기록)

  - `window.history`로 접근

  - 현재 페이지를 기준으로 기록 내의 앞, 뒤, 특정 위치 이동 메서드 제공

  - state 객체 (현재 세션에 연결할 상태 저장)가 존재해 페이지 이동 시 기억해야 할 값들 저장 가능

    ```js
    history.forward();
    history.back();

    history.go(-1); // = back
    history.go(1); // = forward
    history.go(0); // 새로고침

    history.pushState({ name: "nawon" }, "", "/detail/1"); // state, title, url 순
    ```

- **Location** 객체

  - 현재 페이지의 url, 프로토콜, 호스트네임, 포트 번호 등등,,

  - 현재 페이지의 위치와 관련된 정보

  - `window.location` , `document.location` 으로 접근

  - href (온전한 url), port (포트 번호), pathname (/ 뒤 경로), search (? 뒤 쿼리스트링)

- **navigator** 객체

  - 사용자 (클라이언트) id 및 상태 (브라우저 이름, 모바일 사용 여부, 버전)

  - `window.navigator` 또는 `navigator` 로 접근

  - 객체가 제공하는 정보는 브라우저마다 다를 수 있음

<div style="margin: 50px"></div>

### Web Storage

---

- 사용자 (클라이언트 = 브라우저) 쪽에 **키:값** 쌍으로 이루어진 정보 저장하는 방법

- **localStorage** 와 **sessionStorage** 존재

- 웹 스토리지를 통해 저장한 데이터는 HTTP 헤더를 통한 조작 불가능 (쿠키와 다른 점) + 서버로 전송 안됨

- 도메인이나 포트가 동일할지라도, 프로토콜이 다르면 저장된 데이터 접근 불가능

- 적용 가능한 예 : 개개인에 맞춰진 UI 상태 저장 (게시물 임시 저장, 다크 모드 상태 저장)

  ```js
  localStorage.setItem("USER_ID", 1); // 키:값 저장
  localStorage.getItem("USER_ID"); // 키에 해당하는 값
  localStorage.key(0); // index에 해당하는 키 값
  localStorage.removeItem("USER_ID"); // 키에 해당하는 값 삭제

  localStorage.clear(); // 모든 키:값 쌍 삭제
  localStorage.length; // 저장된 개수
  ```

  - 값은 모두 문자열로 저장

  - `JSON.stringify()`,` JSON.parse()` 를 이용하면 객체 형태로 저장하고 다시 객체 형태로 가져오기 가능

<div style="margin: 20px"></div>

- **localStorage** vs **sessionStorage** 차이점

  | 종류           | 특징                                                                                                                               |
  | -------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
  | localStorage   | origin이 같으면 여러 탭/창에 데이터 공유, 세션 이후에도 지속 (컴퓨터 종료 or 브라우저 종료해도 지속)                               |
  | sessionStorage | 하나의 페이지 세션이 유지되는 동안 origin 별로 따로 스토리지 관리, 다른 세션 or 컴퓨터 종료 or 브라우저 종료 시 데이터 접근 불가능 |

- storage 이벤트

  ```js
  window.addEventListner("storage", (e) => {
    console.log(e);
  });
  ```
