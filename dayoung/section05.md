# section 05. 예외
## 예외를 다루는 방법
예외 
* 정상적인 프로그램 흐름을 방해하는 사건. 예외적인 상태에서만 사용
* 많은 경우 프로그램 오류, 버그때문에 발생.

예외가 발생하면
* 예외 상황을 복구해서 정상적인 흐름으로 전환할 수 있는가
  * 재시도
  * 대안 -> 똑같은걸 재시도하는게 아니라 다른 대안을 찾는것
* 버그인가?
  * 예외가 발생한 코드의 버그인가?
  * 클라이언트의 버그인가?
* 제어할 수 없는 예외상황인가?


예외를 잘못 다루는 코드
* 예외를 무시하는 코드
  * 비어있는 catch 블록 등... 예외를 아예 무시하는 코드
* 무의미하고 무책임한 throws

예외의 종류
* Error
  * 시스템에 비정상적 상황 발생
* Exception
  * catch나 throws를 강요
  * Checked Exception
    * 컴파일러가 강제로 예외처리를 요구
    * IOException, SQLException 등
* RuntimeException
