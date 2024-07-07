# 01 스프링 개발 시작하기
***


## PaymentService 개발하기
- 해외직구를 위한 원화 결제 준비 기능 개발
- 주문번호, 외국 통화 종류, 외국 통화 기준 결제 금액을 전달 받아서 다음의 정보를 더해 Payment를 생성한다.
    - 적용 환율
    - 원화 환산 금액
    - 원화 환산 금액 유효시간

- PaymentService.prepare() 메소드로 개발
    - Payment 오브젝트 리턴.


### 01. build.gradle
- Gradle 빌드 시스템에서 사용되는 설정 파일
- build.gradle 파일을 통해 프로젝트의 종속성, 플러그인, 빌드 스크립트 등을 정의
- Gradle은 자동화된 빌드 도구로, 프로젝트의 빌드, 테스트, 배포 등을 관리하는 데 사용


### 02. https://open.er-api.com/v6/latest/USD
<img src="https://i.ibb.co/M54r3X2/2024-07-07-8-01-45.png" style="zoom:50%;" />
- 미국 달러(USD)의 최신 환율 정보를 제공하는 API
- 이 URL을 통해 다양한 통화에 대한 실시간 환율 데이터를 받을 수 있다.
- API는 마지막 업데이트 시간과 다음 업데이트 예정 시간 등을 포함하며, ExchangeRate-API에서 제공하는 서비스이다.
```cmd
:: 지정된 URL에 GET 요청을 보내고 요청 및 응답의 모든 세부 정보를 터미널에 출력
http -v https://open.er-api.com/v6/latest/USD
```



### 03. BigDecimal 클래스

> Java의 기본 자료형인 float과 double은 유한한 비트로 무한 소수 또는 매우 작은 소수점을 표현하기 때문에 정밀도의 한계가 있으며, 반복되거나 복잡한 계산에서 오차가 커질 수 있다.

- Java에서 임의 정밀도의 부동 소수점 수를 표현하기 위해 사용
- BigDecimal 객체는 불변(immutable)으로, 한 번 생성된 객체는 수정할 수 없어 새로운 값은 항상 새로운 객체로 반환
- add, subtract, multiply, divide와 같은 다양한 산술 연산 메소드를 제공



### 04. Record 클래스
- 간결하고 불변하는 데이터 클래스를 작성하기 위해 도입된 새로운 클래스 타입
- 주로 데이터 전달 객체(DTO)를 만들 때 사용되며, 자동으로 생성자, 접근자 메서드(getter), equals(), hashCode(), toString() 메서드를 생성



### 기타 꿀팁
```
프로젝트 목록으로 이동
command(⌘) + 1
```
```
디렉토리, 패키지, 클래스 등 생성 목록 보기
command(⌘) + N
```
