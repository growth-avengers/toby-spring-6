# 오브젝트

- 클래스의 인스턴스
- 배열

# 의존관계

client ---> supplier (client가 supplier를 의존한다)
- client가 제대로 작동하려면 supplier가 필요
- client가 supplier를 사용, 호출, 생성, 인스턴스화, 전송
- supplier가 변경되면 client 코드도 영향을 받는다

# 관심사의 분리 (Separation of Concerns, SoC)

관심사는 동일한 이유로 변경되는 코드의 집합

## 메소드 추출 (refactor - extract method)
리팩토링: 기존의 코드를 외부의 동작 방식에는 변화 없이 내부 구조를 변경해서 재구성하는 작업

## 상속을 통한 확장 - `abstract`
상속하는 클래스는 상위 클래스 이름을 뒤에 붙여서 쓴다

- **한계**: 기능이 많아질수록 상속해야 하는 기능들이 많아진다

## 클래스의 분리
메소드 안에서 오브젝트가 초기화되면 메소드 호출마다 오브젝트 초기화 - 비효율

그걸 밖으로 빼서 빈 생성자 안에서 한 번만 초기화
- **한계**: WebApiExRateProvider 말고 다른 클래스를 쓰고 싶을 경우 클래스를 사용하는 부분들을 다 일일이 바꿔줘야 한다

예) `exRateProvider.getWebExRate(currency)`

## 인터페이스 도입
`getExRate()`를 인터페이스에 설정

인터페이스 안 메소드들은 자동적으로 public 
`getWebApiExRate`가 아닌 공통된 메소드인 `getExRate`를 쓸 수 있다

- **한계**: 사실상 의존 관계는 `PaymentService - WebApiExRateProvider`가 된다

## 관계 설정 책임의 분리
관계 설정의 책임을 Client가 가져가게 된다. 

## 오브젝트 팩토리
Client에서 요청하는 걸 오브젝트 팩토리에서 대신 해준다

[여기서 사용된 원칙과 패턴]

### 개방 폐쇄 원칙 (OCP)
- 클래스나 모듈은 확장에는 열려있어야 하고 변경에는 닫혀있어야 한다. 

### 높은 응집도와 낮은 결합도
- **응집도**가 높다는 것은 하나의 모듈이 하나의 책임 또는 관심사에 집중되어 있다는 뜻. 변화가 일어날 때 해당 모듈에서 변하는 부분이 크다. 책임과 관심사가 다른 모듈과는 낮은 결합도, 즉 느슨하게 연결된 형태를 유지하는 것이 바람직하다.

### 전략 패턴
자신의 기능 맥락(Context)에서, 필요에 따라서 변경이 필요한 알고리즘을 인터페이스를 통해 통째로 외부로 분리시키고, 이를 구현한 구체적인 알고리즘 클래스를 필요에 따라서 바꿔서 사용할 수 있게 하는 디자인 패턴. `Collections.sort()`는 정렬에 사용할 전략 오브젝트를 전달받아서 사용한다.

### 제어의 역전 (IoC, Inversion of Control)
제어권 이전을 통한 제어 관계 역전 - 프레임워크의 기본 동작 원리

`PaymentService -> Client -> ObjectFactory`

### 스프링 컨테이너와 의존관계 주입
스프링의 `BeanFactory`가 앞에서 만든 `ObjectFactory`가 제공하던 기능을 대체한다. 

구성정보를 가져오는 다른 방법: `@Component`, `@ComponentScan`

### 컨테이너
애플리케이션을 구성하는 오브젝트를 만들어서 담아두고 필요할 때 사용하도록 제공하는 기능을 담당하는 것을 컨테이너라고 부른다. 보통 오브젝트를 보관하는 것뿐 아니라 생명주기(lifecycle)까지 담당한다. 스프링 컨테이너는 빈이라고 부르는 오브젝트를 생성하고 의존관계를 설정하는 것까지 담당한다.

### 싱글톤 레지스트리

#### 싱글톤 패턴
전역적 접근, 유일한 인스턴스

싱글톤 패턴(Singleton Pattern)은 소프트웨어 디자인 패턴 중 하나로, 클래스의 인스턴스를 하나만 생성하고, 이 인스턴스에 전역 접근을 제공하는 패턴이다. 싱글톤 패턴을 사용하면 특정 클래스의 객체가 애플리케이션 전체에서 공유되는 하나의 인스턴스만 갖도록 보장할 수 있다.

#### 싱글톤 패턴의 단점
- private 생성자를 가지고 있기 때문에 상속할 수 없다
- 싱글톤은 테스트하기 힘들다
- 서버 환경에서는 싱글톤이 하나만 만들어지는 것을 보장하지 못한다
- 싱글톤의 사용은 전역 상태를 만들 수 있기 때문에 바람직하지 못하다

#### 싱글톤 레지스트리
스프링은 하나의 오브젝트만 만들어져야 한다는 필요를 충족하면서도 싱글톤 패턴을 사용해서 만들었을 때의 단점을 가지지 않도록 컨테이너 레벨에서 하나의 오브젝트만 만들어지는 것을 보장하는 기능을 제공한다.

# 데코레이터 패턴
데코레이터 패턴(Decorator Pattern)은 객체 지향 설계 패턴 중 하나로, 주어진 객체에 새로운 기능을 추가할 수 있는 유연한 방법을 제공한다. 이 패턴은 상속을 사용하지 않고도 동적으로 기능을 추가하거나 변경할 수 있게 해준다. 데코레이터 패턴은 객체를 래핑(wrapping)하는 데코레이터 클래스를 사용하여 원래 객체의 인터페이스를 유지하면서 기능을 확장한다.

# 의존성 역전 원칙 (DIP - Dependency Inversion Principle)
1. 상위 수준의 모듈은 하위 수준의 모듈에 의존해서는 안 된다. 둘 모두 추상화에 의존해야 한다.
2. 추상화는 구체적인 사항에 의존해서는 안 된다. 구체적인 사항은 추상화에 의존해야 한다.

## 방법 - 상위 모듈에 인터페이스 두기
하위 모듈에서 상위 모듈을 의존하게 된다.


