### fetch

---

- fetch() 함수는 접근하려는 url과 옵션 객체를 매개변수로 가짐

- 옵션 객체에는 HTTP 메서드, HTTP 헤더, body 등을 넣어줌

- fetch() 함수를 호출하면, 브라우저는 원하는 요청을 보내고, 프로미스를 반환함

- 프로미스를 반환하기 때문에 이 역시도 프로미스 체이닝과 await 문 사용 가능

- 단, 반환되는 프로미스 객체는 HTTP 상태 값이 404 / 500 이더라도 거부되지 않기 때문에 HTTP 상태 코드에 따라 응답을 처리하려면 response 객체의 ok 또는 status 프로퍼티를 활용할 것

- response 객체의 메서드 (전부 응답 결과를 가공하는 메서드)

  | 종류          | 용도                      |
  | ------------- | ------------------------- |
  | text()        | 텍스트 반환               |
  | json()        | json 형태로 반환          |
  | formData()    | FormData 객체 형태로 반환 |
  | blob()        | Blob 형태로 반환          |
  | arrayBuffer() | ArrayBuffer 형태로 반환   |

- 기본 형태

  ```js
  fetch(url, options)
    .then((res) => {
      console.log(res);
    })
    .catch((e) => {
      console.log(e);
    });

  const result = await fetch(url, options);
  ```

- 옵션 적용 예시

  ```js
  fetch(url, {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
    },
    body: info,
  });
  ```
