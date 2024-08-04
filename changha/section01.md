# BigDecimal 클래스
## 정의
- BigDecimal은 부동 소수점 연산을 정확하게 할 수 있는 클래스이다.
- double이나 float은 정확한 값을 표현하지 못할 수 있지만 BigDecimal은 정확한 값을 표현할 수 있다.
## 다른 기본형과 비교 
### 왜 BigDecimal을 사용해야 하는가?
1. 정밀도, 정확성
    - double, float은 정밀도가 떨어질 수 있다. (이진 부동 소수점 사용하므로)
    - BigDecimal은 정확한 값을 표현할 수 있다. (금융 계산 이용할 때 사용)
2. 데이터 크기 (메모리 사용량)
    - double, float은 8byte, 4byte
    - BigDecimal은 16byte 이상 (내부적으로 임의의 길이를 가지는 배열을 사용함, 크기 유동적)
3. 속도
    - double, float이 빠르다.(하드웨어 수준에서 지원하므로 빠른 계산)
    - BigDecimal은 느리다.(객체 생성 및 메모리 관리를 포함하여 더 복잡한 연산을 수행하므로)

    