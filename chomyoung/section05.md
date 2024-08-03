# Section 5: 예외

## 강의 내용 정리

<hr/>

### 예외 대처
- 정말 예외적인 상황에만 예외 사용(제어할 수 없는 예외상황 등)하는가?
- 예외 상황을 복구해서 정상적인 흐름으로 전환할 수 있는가?
    - 외부 통신 대처: 재시도 혹은 대안 준비
- 예외의 책임이 누구인가?
- 예외의 종류가 무엇인가?
    1. 시스템 비정상적인 상황
    2. checked Exception
    3. unchecked Exception

<br/>

### 예외의 추상화 by 스프링
- 사용 기술에 따라 같은 문제에 대해 다른 종류의 예외 발생
    - 문제: 이를 각각 대응해야하는 문제
    - 스프링의 대처: 적절한 예외 추상화와 예외 번역
    - 예시: JPA를 이용한 order 저장

- DB와 JPA
    - Java에서 오브젝트와 DB를 연결하려면 DateSource 라는 오브젝트가 필요하다.
    - SQL문을 만들어서 DataSource를 통해 데이터를 주고받고 하려면 JDBC라는 java표준을 사용해야한다.
    - 다만 JDBC는 SQL문이 있어야 사용가능하기에 매번 Order를 SQL문으로 변경해주는 작업이 필요하다. 이를 간편하게 해주는 것이 JPA
    - 자바 오프젝트 ↔ DB 변환해줄 때 사용되는 것이 EntityManager(변환 담당)

- 트랜잭션
    - 안전한 처리
        - 만약 롤백을 안전하게 사용하고 싶다면, if 트랜잭션이 active일때
        - finally에서 em.close (안전하게 사용하고 싶다면, if(em.isOpen()) 이런식으로 해도 된다.

- 결론: 스프링 데이터 엑세스 예외처리 DataAccessException
    - JDBC SQLException
        - 대부분의 DB 기술들이 사용한다.
        - 다만 잘 구분하지않아서 기술마다 에러 코드 등이 달라질 수 있다.
    - DataAccessException는 에러 코드와 데이터 엑세스 기술에 독립적인 예외구조이며, 적절한 예외번역 도구 제공

<br/>

## 느낀점

<hr/>

- 예외를 잘 처리하는 것이 중요하다!
    - checkedException 관리
        - 점점 checkedException을 사용하지않으려 한다. catch 대충 혹은 throws 남발
- MainMethod 역할을 DataClient같은 걸로 두어서 진행하는 것도 좋다.
- 체계적인 예외 구조를 만들고 적절한 예외 처리 방법을 사용하고 있는지 살피자. 스프링이 이를 강제한다. 케이스에 따라 필요한 경우 잘 처리하기위해 단순한 exception으로만 만들어선 안된다.