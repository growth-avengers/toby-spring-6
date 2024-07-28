# 템플릿 메서드 패턴이란?
## 정의 
- 여러 클래스에서 공통으로 사용하는 메서드를 템플릿화 함
- 하위 클래스마다 세부 동작 사항을 다르게 구현함 

## 사용 시기
- 클라이언트가 알고리즘의 특정 단계만 확장하고, 전체 알고리즘이나 해당 구조는 확장하지 ㅇ낳을 때 
- 여러 클래스에서 공통으로 사용하는 메서드를 템플릿화 함

## 구현 방법
- 추상 클래스를 확장한 구현 클래스를 만들어 구현함
- 추상 클래스에 템플릿 메서드를 정의하고, 하위 클래스에서 구현할 메서드를 추상 메서드로 선언함
- 템플릿 메서드에서는 추상 메서드를 사용함

## 예제
- 템플릿 메서드 패턴을 사용한 예제는 다음과 같음
```java
public abstract class AbstractClass {
    public void templateMethod() {
        abstractMethod1();
        hookMethod1();
        if (hookMethod2()) {
            abstractMethod2();
        }
        abstractMethod3();
    }
    protected abstract void abstractMethod1();
    protected abstract void abstractMethod2();
    protected abstract void abstractMethod3();
    protected void hookMethod1() {}
    protected boolean hookMethod2() {
        return true;
    }
}
```
```java
public class ConcreteClass extends AbstractClass {
    protected void abstractMethod1() {
        System.out.println("abstractMethod1 구현");
    }
    protected void abstractMethod2() {
        System.out.println("abstractMethod2 구현");
    }
    protected void abstractMethod3() {
        System.out.println("abstractMethod3 구현");
    }
    protected void hookMethod1() {
        System.out.println("hookMethod1 구현");
    }
    protected boolean hookMethod2() {
        return false;
    }
}
```
```java
public class Client {
    public static void main(String[] args) {
        AbstractClass obj = new ConcreteClass();
        obj.templateMethod();
    }
}
```

# ApiExecutor 분리를 왜 해야 하나? 
## 이유
- 개방 폐쇄 원칙을 지켜야 함 
- 결합도를 낮추는 게 중요함, 결합도가 높으면 유지보수가 어려워짐
- ApiExecutor가 변경되면, Client도 변경되어야 함
- 그래서 리팩토링할 때 인터페이스, 클래스를 이용한 추상화 작업이 필요 

## 개방 폐쇄 원칙이 뭐지?
- 소프트웨어 요소는 확장에 대해서는 열려 있어야 하지만, 변경에 대해서는 닫혀 있어야 한다는 원칙
- 즉, 기존 코드를 변경하지 않고 새로운 기능을 추가할 수 있어야 함
- 이를 위해 인터페이스, 추상 클래스를 사용함

# ApiExecutor 분리 방법
## 방법
- 인터페이스를 만들어 ApiExecutor를 구현함
- Client에서는 인터페이스를 사용함
- 이렇게 하면 ApiExecutor가 변경되어도 Client는 변경하지 않아도 됨
- 이렇게 하면 결합도를 낮출 수 있음

## 예제
- ApiExecutor를 인터페이스로 만들어 구현한 예제는 다음과 같음
```java
public interface ApiExecutor {
    void execute();
}
```
```java
public class SimpleApiExecutor implements ApiExecutor {
    public void execute() {
        System.out.println("ApiExecutorImpl 실행");
    }
}
```
```java
public class Client {
    public static void main(String[] args) {
        ApiExecutor apiExecutor = new SimpleApiExecutor();
        apiExecutor.execute();
    }
}
```

# 콜백함수란?
## 정의
- 어떤 함수에 인자로 전달되어, 그 함수 내부에서 특정 작업이 완료된 후 호출되는 함수
- 콜백함수는 다른 함수의 인자로 사용되는 함수를 말함

## 사용 이유
- 트랜잭션 관리
**- 템플릿 메서드 패턴 : 콜백을 통해 세부 작업을 사용자에게 위임** (지금 상황에 알맞는 이유)
- 비동기 작업 

## 구현 방법
- 인터페이스를 만들어 콜백함수를 구현함
- 콜백함수를 사용할 클래스에서 인터페이스를 구현함
```java
public interface ApiExecutor {
    void callback();
}
```

```java
import java.math.BigDecimal;

public class WebApiExRateProvider {

    public BigDecimal getExRate() {
        //~~~
        return runApiForExRate(new SipmleApiExecutor());
    }

    public static void runApiForExRate(ApiExecutor apiExecutor) {
        //~~~
        apiExecutor.callback();
    }
}
```
```java
public class SimpleApiExecutor implements ApiExecutor {
    public void callback() {
        System.out.println("ApiExecutorImpl 실행");
    }
}
```
```java
public class Client {
    public static void main(String[] args) {
        WebApiExRateProvider webApiExRateProvider = new WebApiExRateProvider();
        webApiExRateProvider.getExRate();
    }
}
```
- 람다 식으로 익명 클래스를 사용할 수도 있음(But, 람다식은 인터페이스에 추상 메서드가 하나만 있을 때 사용 가능)


