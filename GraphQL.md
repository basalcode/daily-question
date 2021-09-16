GraphQL은 왜 사용할까?
===
REST API가 아닌, GraphQL을 사용하는 이유에 대해 알아보자.
---

### 1. 원하는 정보만 불러올 수 있다.
GraphQL은 요청한 데이터만 서버로부터 불러올 수 있다.<br /> 
<br />
REST API를 사용하면서 겪는 Over-fetching이나 Under-fetching과 같은 문제는 네트워크 비용 증가와 데이터를 필요에 맞게 재가공해야한다는 문제가 있는데 이를 해결할 수 있다.<br />

### 2. End point가 하나다.
GraphQL은 한번의 HTTP 요청(End point)으로 필요한 데이터를 모두 요청할 수 있다는 장점이있다.<br />
<br />
REST API의 경우, 페이지를 구성하는 정보를 불러오기 위해 여러번의 API 호출이 발생하게 되는데, 리소스를 가져오는 API를 URL 경로별로 구현해줘야한다.<br />

### 3. Apollo
GraphQL의 상태를 관리해주는 Apollo라는 멋진 프로젝트가 있다.<br />
Apollo를 사용하게되면 별도의 Action, Reducer를 작성하지 않아도 필요한 리소스를 컴포넌트에서 사용할 수 있다.<br />
<br />
Redux를 사용하게되면 Action과 Reducer 그리고 미들웨어(Redux saga와 같은)에 대한 코드를 작성해야한다는 불편함이 있다.<br />


### 4. GraphQL의 단점
* HTTP 캐싱을 그대로 사용하는 것이 불가능하다.<br />
  영속 쿼리(persisted query) 또는 아폴로 엔진(Apollo Engine)등의 대안이 있다.<br />
* 파일 업로드를 직접 개발해야한다.<br />
* 클라이언트 요청에 대한 필터링이 어렵다.