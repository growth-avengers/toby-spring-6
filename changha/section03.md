# Array와 List의 차이점 
## Array
- 배열은 고정된 크기를 가지고 있으며, 크기를 변경할 수 없다.
- 배열은 기본적으로 같은 타입의 데이터만 저장할 수 있다.
- 배열은 연속된 메모리 공간에 순차적으로 데이터를 저장한다.

## List
- List는 크기가 가변적이다.
- List는 다양한 타입의 데이터를 저장할 수 있다.
- List는 연속된 메모리 공간에 순차적으로 데이터를 저장하지 않는다.
- List는 데이터를 추가하거나 삭제할 때마다 메모리를 재할당하고 데이터를 복사해야 하는 작업이 필요하다.

## 비교
| Array | List |
|---|---|
| 고정된 크기 | 가변적인 크기 |
| 같은 타입의 데이터만 저장 | 다양한 타입의 데이터 저장 가능 |
| 연속된 메모리 공간에 순차적으로 데이터 저장 | 연속된 메모리 공간에 순차적으로 데이터 저장하지 않음 |

## List의 종류
- ArrayList
- LinkedList
- Vector

-----------------~
# @ExtendWith, @ContextConfiguration 쓰임새 

## @ExtendWith
- 단위 테스트에 공통적으로 사용할 확장 기능을 선언해주는 역할을 한다.
- JUnit5와 Spring을 통합하여 Spring 테스트 컨텍스트를 사용할 수 있도록 함 

## @ContextConfiguration
- 테스트할 때 주로 사용하는 어노테이션
- (classes = TestPaymentConfig.class)는 TestPaymentConfig 클래스에서 정의한 설정을 기반으로 테스트 컨텍스트를 구성한다는 의미

-----------------

# (테스트와 DI 2)[13분 15초쯤] @ExRateProviderStub 대신 @ExRateProvider 를 사용한다면
- @ExRateProvider 타입으로 한다면 ((ExRateProviderStub) exRateProviderStub).setExRate(valueOf(500));
- 위와 같은 식으로 형변환을 해야 함 
- setExRate는 ExRateProviderStub에만 있는 메소드이기 때문에
- @ExRateProviderStub 타입으로 한다면 형변환을 하지 않아도 됨
