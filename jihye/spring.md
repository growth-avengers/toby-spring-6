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
