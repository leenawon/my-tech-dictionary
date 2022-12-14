### HTTP 메시지

---

HTTP 메시지는 한마디로 애플리케이션 사이에서 주고 받은 데이터 블록을 뜻한다.
클라이언트가 서버에게 보내는 요청, 서버가 클라이언트에게 보내는 응답 모두 HTTP 메시지인 것이다.
메시지는 시작줄, 헤더, 본문으로 구성되며, 어떤 메시지인지인지 시작줄에 나타나있고, 속성은 헤더 부분에, 데이터는 본문에 담고 있다.

<div style="margin: 30px"></div>

### HTTP 메시지 문법

---

#### 1. 요청 메시지

```
시작줄 - [메서드] [요청 URL] [버전]
헤더 - [헤더]
본문 - [본문]
```

- 메서드 : 클라이언트가 서버에게 요청하는 동작 (한 단어)
- 요청 URL : 요청의 대상이 되는 리소스
- 버전 : HTTP 버전

<div style="margin: 30px"></div>

#### 2. 응답 메시지

```
시작줄 - [버전] [상태코드] [사유구절]
헤더 - [헤더]
본문 - [본문]
```

- 버전 : HTTP 버전
- 상태 코드 : 3자리 숫자로, 요청 중 어떤 일이 일어났는지를 나타냄
- 사유 구절 : 상태 코드의 의미를 부연 설명해주는 짧은 문구

- 공통
  - 헤더 : 이름, 콜론(:), 공백(선택), 어떤 값, CRLF(줄바꿈 문자열)
  - 본문 : 데이터 블록 (모든 메시지가 본문을 가지고 있지는 않음)

<div style="margin: 30px"></div>

#### 3. 시작줄

시작줄은 모든 HTTP 메시지의 시작을 알린다. 요청 메시지에서의 시작줄은 무엇을 해야하는지를 나타내고, 응답 메시지의 시작줄은 무슨 일이 일어났는지를 말해준다.

#### (1) 요청줄 (요청 메시지의 시작줄) : 메서드, 요청 URL, HTTP 버전

- 메서드 : 서버에서 수행해주었으면 하는 동작

  | 메서드  | 의미                                             |
  | ------- | ------------------------------------------------ |
  | GET     | 데이터를 가져옴                                  |
  | HEAD    | 헤더만 가져옴                                    |
  | POST    | 데이터를 서버로 보냄                             |
  | PUT     | 요청 메시지에 담긴 데이터를 서버에 저장          |
  | TRACE   | 메시지가 프록시를 거쳐 서버에 도달하는 과정 추적 |
  | OPTIONS | 서버가 메서드를 수행할 수 있는지 확인            |
  | DELETE  | 데이터 제거                                      |

#### (2) 응답줄 (응답 메시지의 시작줄) : 상태 코드, 결과 데이터

- 상태 코드 : 요청한 동작에 대한 수행 결과를 나타내는 3자리 숫자

  | 상태 코드 | 의미            | 상세                                                                                                             |
  | --------- | --------------- | ---------------------------------------------------------------------------------------------------------------- |
  | 100-101   | 정보            |
  | 200-206   | 성공            | 200(OK) : 성공                                                                                                   |
  | 300-305   | 리다이렉션      |
  | 400-415   | 클라이언트 에러 | 401(Unauthorized) : 사용자 이름과 비밀번호를 입력해야함, 405(Not Found) : 요청 URL에 해당하는 리소스를 찾지 못함 |
  | 500-505   | 서버 에러       |

<div style="margin: 30px"></div>

### TCP 커넥션

---

#### 브라우저가 겪는 과정

```
브라우저는 호스트명(예: www.naver.com)을 추출한다.
-> 해당 호스트명에 대한 ip 주소를 찾는다.
-> 포트번호(예: 80)를 추출한다.
-> 브라우저는 얻은 ip 주소의 얻은 포트 번호로 TCP 커넥션을 맺는다.
-> 브라우저는 서버로 HTTP 요청 메시지를 보낸다.
-> 브라우저는 서버로 부터 전달받은 응답 메시지를 읽는다.
-> 커넥션을 끊는다.
```
