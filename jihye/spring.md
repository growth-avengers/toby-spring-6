# 섹션1 스프링 개발 시작하기
## 스프링부트를 왜 쓸까?
Spring Boot makes it easy to create stand-alone, production-grade Spring based Applications that you can "just run". -> 스프링부트는 단지 실행만 하면 되는 스프링 기반의 애플리케이션을 쉽게 만들 수 있다.
- 복잡한 설정 간소화
    - 자동 설정(AutoConfiguration)
- 미리 설정된 Starter 프로젝트를 제공해서 자동으로 호환되는 버전을 관리해준다.
- 내장 서버 제공으로 간단하게 배포하고 실행할 수 있음

## 소수점 숫자를 쓸 때 float, double 대신 BIgDecimal 쓰는 이유는 뭘까
### BIgDecimal 사용 이유
- 정확한 계산과 정밀도 유지 때문이다.
  float,double 사용 이유
- float과 double은 부동 소수점 수를 표현하는데 사용하고 컴퓨터 하드웨어에서의 효율적인 연산을 위해 설계됐음
    - 근사치를 사용하기 때문에 소수점 연산을 하는 경우에 문제가 발생할 수 있음

### BIgDecimal 단점
- float,double 보다 사용법이 복잡하다. 연산 메서드를 사용해야 함
- float,double 보다 연산 속도가 느리고 더 많은 메모리 사용

## Java record 장점, 단점?
### 장점
- 간결성
    - 생성자, getter, equals, hashCode, toString 등의 메서드 자동 생성
- 불변성 보장
    - 자동으로 final 변수로 선언됨, setter 메소드 없음 -> 데이터 무결성을 유지하는데 도움을 줌
### 단점
- 불변성을 강제하기 때문에 가변 객체가 필요한 경우 사용할 수 없음
- record는 다른 클래스를 상속할 수 없고 상속 받을 수도 없다.
    - 상속을 통한 공통 기능 공유 불가 

## 섹션2 오브젝트와 의존관계
### 자바에서 오브젝트란?
- 클래스의 인스턴스가 오브젝트다.
- 자바에서는 배열도 오브젝트이다.

### 객체지향 원칙(SOLID) 중 OCP란 무엇인가요?
- Open-Closed Principle
- 클래스나 모듈은 확장에는 열려 있어야 하고 변경에는 닫혀 있어야 한다.
  - 어떤 클래스는 기능을 확장할 때 그 클래스의 코드는 변경되면 안된다.

### 높은 응집도와 낮은 결합도란?
- 응집도가 높다는 건?
  - 하나의 모듈 혹은 클래스가 하나의 책임/관심사에 집중되어 있다는 뜻
  - 특정 관심사의 요구사항이 변경된다면 그 하나의 모듈 혹은 클래스만 수정해서 대응할 수 있어야 함
    - -> 변화가 일어날 때 비용이 적게듬
- 낮은 결합도란?
  - 책임과 관심사가 다른 모듈/클래스와 느슨하게 연결하는 것
  - 높은 결합도를 가진다면 연결된 모듈/클래스에 변화가 발생 했을 때 연결된 것들에도 큰 변화가 요구될 수 있음

### DIP란?
- Dependency Inversion Principle
- 의존성 역전 원칙
- 상위 수준의 모듈은 하위 수준의 모듈에 의존해서는 안된다.
  - 하위 수준의 모듈이 상위 수준의 모듈에 의존해야 한다.
  - 둘 모두 추상화(인터페이스) 에 의존해야 한다.
    - 모듈이란 소프트웨어 시스템을 연관 관계가 있는 작은 단위로 쪼개놓은 것
- 추상화는 구체적인 사항에 의존해선 안된다.
  - 구체적인 사항은 추상화에 의존해야 한다.

## 섹션3 테스트
### Mock 테스트와 Stub 테스트의 차이점은?
우선 테스트 대역에서 대해서 알아야 한다.
- 테스트 대역
  - 의미: 테스트 하려는 객체가 다른 객체들과 여러 관계가 얽혀 있어 사용하기 힘들 때 대체할 수 있는 객체
  - 종류: Dummy, Stub, Spy, Mock, Fake ... 

#### Mock 
- 행위 검증 진행
- 호출에 대한 기대를 명세하고, 내용에 따라 동작하도록 프로그래밍 된 객체

#### Stub
- 상태 검증 진행
- 인스턴스화 하여 구현한 가짜 객체를 이용해 실제 동작하는 것처럼 보이게 만드는 객체
- 테스트에서 호출된 요청에 대해 미리 준비해둔 걸로 응답한다
- 인터페이스나 클래스를 최소환으로 구현 


#### Mock/Stub 차이점
검증 대상이 다르다.
- stub은 상태 검증
  - 상태 검증이란? 메소드가 수행된 후 객체 상태를 확인해서 올바르게 동작 했는지를 확인하는 검증법
- mock은 행위 검증
  - 행위 검증이란? 메소드의 리턴값으로 판단할 수 있는 경우, 특정 동작을 수행하는지 확인하는 검증법

## 섹션4 템플릿
### 템플릿의 의미는?
- 변경될 가능성이 거의 없는 코드를 변경 가능성이 큰 부분과 분리시켜 활용하는 것

### 콜백이란?
- 오브젝트를 메서드 파라미터로 넘기는 것 
- 콜백을 넘겨 받는 함수는 콜백 함수를 필요에 따라 실행 시점을 조정할 수 있다.

### 템플릿과 콜백 형태로 만드는 이유는?
- 재사용 목적, 필요하다면 콜백을 변경하는 것도 가능 

## 섹션5 예외
### 예외 처리 방법은 어떤 게 있나
- 크게 3가지 방법이 있음
- 복구, 회피, 전환
- 복구는 예외 상황을 파악하고 문제를 해결해서 정상으로 돌려 놓는 것
  - 단순히 에러 메시지 노출하는 건 복구가 아님
  - 예외로 기본 작업 흐름이 불가능할 때 다른 작업 흐름으로 유도하는 것
- 회피는 예외 처리를 자신이 담당하지 않고 호출한 쪽으로 던지는 것
  - 의도가 분명해야 함
- 전환은 예외를 메소드 밖으로 던지는 건데 회피와 다른 점은 적절한 예외로 바꿔서 던진다는 점이다
  - 예외를 처리하기 쉽고 단순하게 만들기 위해 포장하는 목적

## 섹션6 서비스 추상화
### 추상화란 뭘까
- 구현의 복잡함과 세부적인 내용을 감추고 중요한 것만 남기는 것
#### 추상화는 왜 중요할까
- 컴퓨터가 추상화 그 자체임
  - 사용자는 컴퓨터 세부적인 걸 전혀 몰라도 사용하는데 문제가 없음
- 핵심에만 집중할 수 있음 
- 추상화가 잘 되어 있는 코드라면 요구사항이 변경되더라도 변경점이 적을 확률이 높음