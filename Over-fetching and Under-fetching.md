Over-fetching과 Under-fetching이란?
===
원하는 데이터를 적절하게 불러오고 있는가?
---

### 1. Over-fetching
* 필요한 것 보다 많은 정보를 DataBase에서 불러와 Server를 통해 받는 것을 말한다.
* 예를들어, UserName값을 조회하려고 API 호출을 했을 때 서버에서 UserName 외에도 email, phoneNumber, profileImage 등의 정보를 반환하는 것을 말한다.
* 

### 2. Under-fetching
* 한번의 API 호출을 통해서 페이지에 필요한 정보를 모두 불러오기 어려운 경우가 있는데 이를 Under-fetching 이라고 한다.
* 예를들어, 로그인 상태 조회, 알림 내역 조회, 글 목록 조회를 할 때 3번의 API 호출이 필요하다면 Under-fetching이라고 할 수 있다.
