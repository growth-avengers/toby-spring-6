# 트랜잭션 
## 정의 
- 여러 작업을 진행하다가 문제가 생겼을 때 이전 상태로 롤백하는 것 
- AOP방식으로 트랜잭션이 작동한다.
- 여기서 AOP vs 템플릿화 차이점에 대해 궁금했다. 관심사의 분리라는 키워드 때문 
- AOP
  - 목적
    - AOP는 부가적인 관심사를 분리하여 코드의 핵심 비즈니스 로직과 독립적으로 관리할 수 있게 함, 모듈화 함.
    - 트랜잭션, 보안, 로깅, 예외처리 등의 부가적인 관심사를 분리하여 코드의 핵심 비즈니스 로직과 독립적으로 관리할 수 있게 함
    - 트랜잭션의 시작과 종료를 알아서 처리해줌
- 템플릿화
  - 목적
    - 코드의 재사용성과 일관성을 높이기 위해 공통 알고리즘을 정의하고 구체적인 구현을 하위 클래스에 위임함
- 롤백 위치
  - 트랜잭션의 롤백은 트랜잭션의 시작과 종료 사이에 발생한 예외에 대해서만 롤백됨
  - 트랜잭션의 시작과 종료 사이에 발생한 예외가 아니라면 롤백되지 않음
## 정보 
- 스프링에서 auto_increment or sequence로 증가된 값은 rollback되지 않음, 그래서 테스트 할 때는 인메모리(ex. h2) DB를 이용해서 테스트 함.
## 종류
- 프로그래밍 방식
  - 개발자가 직접 트랜잭션을 컨트롤하는 방식
  - `PlatformTransactionManager`를 사용하여 트랜잭션을 컨트롤함
- 선언적 방식
  - `@Transactional` 어노테이션을 사용하여 트랜잭션을 컨트롤하는 방식
  - `TransactionProxyFactoryBean`을 사용하여 트랜잭션을 컨트롤함

# 영속화
## 정의 
- 애플리케이션에서 데이터를 영구적으로 저장하는 과정
- JPA, Hibernate, MyBatis 등이 있음
- JPA는 자바 ORM 기술로, 객체와 관계형 데이터베이스의 매핑을 처리함
- Hibernate는 JPA의 구현체 중 하나로, JPA를 구현한 라이브러리
- MyBatis는 SQL Mapper로, SQL을 직접 작성하여 데이터베이스와 연동함

# DataSource
## 정의
- 데이터베이스와 연결을 위한 객체
- `DataSource` 인터페이스를 구현한 클래스를 사용함
- `DriverManagerDataSource`, `SimpleDriverDataSource`, `SingleConnectionDataSource` 등이 있음
- `DriverManagerDataSource`는 JDBC 드라이버를 사용하여 데이터베이스와 연결함
- `SimpleDriverDataSource`는 `DriverManagerDataSource`의 확장 버전으로, 데이터베이스 연결 정보를 설정할 때 `DriverManagerDataSource`보다 더 많은 설정을 할 수 있음
- `SingleConnectionDataSource`는 하나의 커넥션을 공유하여 사용함
- `DataSource`를 사용하면 커넥션 풀링을 사용할 수 있음
- 커넥션 풀링을 사용하면 커넥션을 미리 생성해 두고 사용자가 요청할 때마다 커넥션을 제공함

