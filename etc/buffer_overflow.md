# Buffer overflow

프로그래밍에서 Buffer overflow(또는 Buffer overrun)이란 어떤 프로그램에서 data를 buffer에 적을 때, buffer의 경계를 넘어 인접한 메모리에까지 overwrite하는 상황을 말한다.
Buffer란 데이터를 잠시 가지고 있거나, 프로그램의 한 부분에서 다른부분으로 이동시킬 때, 또는 한 프로그램에서 다른 프로그램으로 이동시킬 때 사용되는 공간이다.

Buffer overflow는 잘못된 input 때문에 발생할 수 있다. 
준비된 buffer보다 더 많은 양의 데이터를 입력하게 되면 인접한 데이터나 실행 코드가 덮어 쓰여지면 메모리 액세스 오류, 잘못된 결과 및 충돌을 비롯한 잘못된 프로그램 동작이 발생할 수 있다.

[Reference](https://en.wikipedia.org/wiki/Buffer_overflow)

