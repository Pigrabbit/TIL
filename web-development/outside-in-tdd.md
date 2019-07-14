Test-Driven Development라고 하면, implementation code이전에 test code를 작성하는 것을 의미한다.
작성한 test code로 부터 feature의 구현에 대한 feedback을 받을 수 있기 때문에 이 방법이 유용하다.

TDD의 일반적인 접근방법은 red, green, refactor cycle이다. 
Implementation 이전에 test를 작성했으면 test가 fail하고 error message를 return하기 떄문에 **red** phase 상태이다.
그 다음, 작성한 test를 통과하도록 implementation 코드를 추가했으면 **green** status가 된다.
Green 상태가 된 이후에는 추가한 implementation 코드를 최적화한다.
이 단계를 **refactor** phase라고 한다.

# Outside-In TDD

Outside-in TDD는 full-stack web application을 개발할 때 쓰는 방법이다.
일반적인 TDD와 비슷하게 red, green, refactor cycle을 따르지만 한 가지 다른 점이 있다.
Test가 fail한다고 반드시 implementation code를 추가해야 하는 것은 아니라는 점이다.
대신에, 다른 level(view, server, database)에 새로운 functionality를 구현할 필요가 있다는 신호가 될 수 있다.

Testing pyramid의 가장 윗쪽 view에서부터 database로 내려오며 test code를 작성하고 있다고 하자.

이때 test가 아래 level로 유도한다면, 그 아래 level에서 새로 red, green, refactor의 cycle로 TDD를 진행한다. 
원하는 behavior의 구현을 위해 하위 layer로 내려가야 하거나, 또는 현재의 layer로 내려오게된 원인을 완전히 solve 할 때까지 TDD를 계속한다.

하위 layer로 내려오게 된 원인을 모두 해결했다면 다시 testing pyramid 위로 올라갈 차례다.
Database layer에 있다면 server layer로 올라가서 test를 실행하여 변경된 response를 받았는지 확인한다.

이 때 test가 통과한다면, server layer에서 또 다른 red, green, refactor cycle을 시작하거나 view layer로 하나 더 올라가서 test를 진행하면 된다.

그러나 test가 깨진다면, server layer에 implementation을 추가하거나, model layer로 내려가서 다시 TDD를 진행하야 한다.

