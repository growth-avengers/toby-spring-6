# Record
- **불변 객체를 제공**

자동 생성되는 메서드: `record`를 사용하면 다음과 같은 메서드들이 자동으로 생성된다:
- getter 메서드 (result(), rates())
- equals(Object o)
- hashCode()
- toString()

# BigDecimal
`BigDecimal`은 Java에서 숫자를 정확하게 표현하고 계산하기 위해 사용되는 클래스이다.
특히, 부동 소수점 연산의 오차를 피하고 정밀한 계산을 필요로 하는 상황에서 유용하다.

## BigDecimal 사용이 필요한 상황
- **정밀한 소수점 계산**:
  부동 소수점 연산(float와 double)은 근사값을 사용하기 때문에, 정확한 소수점 연산이 필요할 때는 `BigDecimal`을 사용한다.

- **금융 계산**:
  예를 들어, 이자 계산, 통화 변환 등의 작업에서 `BigDecimal`을 사용하여 오차 없이 계산할 수 있다.

- **과학 계산**:
  과학 분야에서는 높은 정밀도가 필요한 계산이 많다. `BigDecimal`은 이러한 상황에서 유용하다.
