# 01 오브젝트와 의존관계
***
## 1. 오브젝트와 의존관계
### 오브젝트
- 클래스를 기반으로 생성된 실제 인스턴스
- 실제로 우리가 프로그램을 실행하면 그때 만들어져서 동작하는 무엇인가

### 클래스
- 객체를 생성하기 위한 설계도
- 객체가 가지는 속성과 행동을 정의

### 의존관계
- 한 클래스나 모듈이 다른 클래스나 모듈을 필요로 하는 관계
- 클래스 A가 클래스 B의 인스턴스를 생성하거나 사용하는 경우, 클래스 A는 클래스 B에 의존
- 클래스 B가 변경되면 클래스 A는 이에 영향을 받음
- 클래스 레벨의 의존관계와 런타임 레벨의 의존관계가 다름

## 2. 관심사의 분리
```java
    public Payment prepare(Long orderId, String currency, BigDecimal foreignCurrencyamount) throws IOException {
        // 환율 가져오기
        URL url = new URL("https://open.er-api.com/v6/latest/" + currency);
        HttpURLConnection connection = (HttpURLConnection) url.openConnection();
        BufferedReader br = new BufferedReader(new InputStreamReader(connection.getInputStream()));
        String response = br.lines().collect(Collectors.joining());
        br.close();

        ObjectMapper mapper = new ObjectMapper();
        ExRateData data = mapper.readValue(response, ExRateData.class);
        BigDecimal exRate = data.rates().get("KRW");
        System.out.println(exRate);

        // 금액 계산
        BigDecimal convertedAmount = foreignCurrencyamount.multiply(exRate);

        // 유효 시간 계산
        LocalDateTime validUntil = LocalDateTime.now().plusMinutes(30);

        return new Payment(orderId, currency, foreignCurrencyamount, exRate, convertedAmount, validUntil);
    }
```

- 각 부분이 독립적으로 변경될 수 있도록 코드도 명확히 분리
- 변경이 되는 시점과 이유가 다른 두 가지가 함께 들어 있는 경우, 유지보수성과 확장성이 떨어짐
1. 환율 정보 가져오기: 웹 API를 호출하여 환율 데이터를 가져오고, 이를 파싱하여 환율 값을 추출
2. 결제 정보 처리: 환율을 사용하여 외화 금액을 원화로 변환하고, 결제 정보를 생성

## 3. 상속을 통한 확장
하지만 여전히 클래스 레벨에서 보면 두 개의 관심사를 가지고 있다. Payment라는 오브젝트를 생성하는 코드를 잘 만들어놨어도 환율을 가져오는 방식이나 여러 매커니즘이 변경되면 전체를 계속 수정해야하기때문에 재사용 관점에서 좋지않다.
- 클래스 분리하고 상속을 통해 확장해줌
```java
public class WebApiExRatePaymentService extends PaymentService {}
```


## 4. 클래스의 분리
상속을 통한 확장은 오히려 코드의 복잡성을 증가시킬 수 있으며, 이로 인해 코드의 재사용성이 떨어질 수 있다.
- 상속을 통한 확장보다는 명확한 클래스 분리를 통해 각 클래스의 역할을 분명히 하는 것이 바람직함
- 클래스의 분리를 통해 각 클래스가 하나의 책임만 가지도록 설계

<img src="https://i.ibb.co/LzntTsv/2024-07-07-10-42-50.png"  />


## 5. 인터페이스 도입
getWebExRate()와 getExRate() 메소드 이름을 통일해준다.

<img src="https://i.ibb.co/q5jsZmq/2024-07-07-10-44-04.png"  />


## 6. 관계설정 책임의 분리
런타임에 의존해서 사용해야 할 클래스에 오브젝트를 의존하는 거지만 그거를 설정하는 책임이 어디에 있는가 그거에 따라서 코드 레벨의 의존 관계도 달라진다. 따라서 의존관계를 설정하는 그 코드를 다른 곳을 분리한다.

## 7. 오브젝트 팩토리
그 안에 또 PaymentService가 다른 클래스 오브젝트와 어떻게 관계를 맺어야 될지에 대한 책임을 분리해준다.

```java
public class ObjectFactory {}
```

## 8. 원칙과 패턴
**개방 폐쇄 원칙(OCP)**
- 클래스나 모듈은 확장에는 열려 있어야 하고 변경에는 닫혀 있어야 한다.
- 어떤 클래스는 이 클래스의 기능을 확장할 때 그 클래스의 코드는 변경되면 안 된다.

**높은 응집도와 낮은 결합도**
- 응집도가 높다는 것은 하나의 모듈이 하나의 책임 또는 관심사에 집중되어있다는 뜻으로 변화가 일어날 때 해당 모듈에서 변하는 부분이 크다.
- 책임과 관심사가 다른 모듈과는 낮은 결합도, 즉 느슨하게 연결된 형태를 유지하는 것이 바람직하다.

**전략패턴**
- 자신의 기능 맥락에서 필요에 따라서 변경이 필요한 알고리즘을 인터페이스를 통해 통째로 외부로 분리시키고 이를 구현한 구체적인 알고리즘 클래스를 필요에 따라 바꿔서 사용할 수 있게 하는 디자인 패턴

**제어의 역전**
- 제어권 이전을 통한 제어관계 역전 - 프레임워크의 기본 동작 원리