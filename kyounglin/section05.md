## 예외

### Error
- 시스템 레벨의 오류로, 프로그램에서 복구할 수 없는 심각한 문제를 나타냄
- 예시: `OutOfMemoryError`, `StackOverflowError`
- 애플리케이션 코드에서 이들을 처리하거나 복구하는 것은 일반적으로 불가능하며, 이를 시도해서도 안 된다

### Exception과 체크 예외
- 애플리케이션 코드에서 복구 가능한 문제를 나타냄
- 예시: `IOException`, `SQLException`
- 예외가 발생할 가능성이 있는 코드에서는 반드시 예외 처리를 해야 한다

### Runtime Exception과 언체크 예외
- 실행 시 발생하는 예외로, 프로그래밍 오류를 나타냄
- 예시: `NullPointerException`, `ArrayIndexOutOfBoundsException`
- 주로 프로그래밍 실수 (예: 잘못된 인덱스 접근, null 참조)로 인해 발생하며, 개발자가 코드를 통해 예외 상황을 방지할 수 있다

## DataSource
- DataSource는 자바에서 데이터베이스와의 연결을 관리하는 데 사용되는 객체이다.
- 다른 별도의 설치 없이 사용 가능하다.

## EntityManager
- EntityManager는 Java Persistence API (JPA)에서 데이터베이스와의 상호작용을 관리
- 엔티티 매니저는 트랜잭션 경계를 지정하고, 데이터베이스 작업을 트랜잭션 내에서 수행한다
- 다음과 같은 구조를 가진다.

## SQLException
- SQLException은 자바 표준 라이브러리 (`java.sql` 패키지)에 포함된 예외 클래스
- SQLException은 체크 예외이므로, 이를 처리하거나 메서드 시그니처에 선언해야 한다

## DataAccessException
- DataAccessException은 언체크 예외 (런타임 예외)
- 이를 처리하기 위해 명시적으로 try-catch 블록을 사용할 필요는 없다.
- 스프링은 다양한 데이터 접근 기술 (JDBC, JPA, Hibernate 등)을 지원하며, 각 기술에서 발생하는 예외를 통합
- 데이터베이스 관련 예외를 추상화하여 특정 데이터베이스 기술에 종속되지 않도록 한다
