# 관계설정 책임의 분리 	
## 정의
- 관계설정이란, 한 클래스 안에 다른 클래스의 객체를 인스턴스 없이 생성하는 것이다. 
- 관계설정 책임의 분리란 객체 사이의 관계를 설정하는 책임을 각 객체에게 나눠주는 것을 말한다.

## 사용 이유 
- 코드에서, PaymentService 내에 생성자 만들 때 Provider를 생성하면 PaymentService가 Provider에 의존하게 된다.
- PaymentService는 Provider에 의존하게 되면 PaymentService가 Provider의 구현에 영향을 받게 된다.
- 그러면 유지보수가 어려워지기 때문에 관계설정 책임의 분리가 필요하다.

## 관계설정 책임의 분리 방법
- PaymentService의 앞 단에 Client를 두고, 
- Client가 Provider를 생성하고, 
- Provider를 PaymentService에게 전달하는 방법이다.



# 오브젝트 팩토리를 사용하는 이유 
## 정의
- 오브젝트 팩토리란, 오브젝트를 생성하는 책임을 가진 팩토리 클래스를 만드는 것이다.

## 사용 이유
- 코드에서, Client가 Provider를 생성하고, Provider를 PaymentService에게 전달하는 방법을 사용하면,
- Client가 PaymentService와 Provider의 생성을 담당하게 되어, Client가 PaymentService와 Provider에 의존하게 된다.
- 그러면 유지보수가 어려워지기 때문에 오브젝트 팩토리를 사용한다.
