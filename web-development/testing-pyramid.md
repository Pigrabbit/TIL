# The Testing Pyramid

Full-stack web application은 매우 크고 복잡하기 떄문에, codebase가 길어지고 user수가 증가하게 되면 버그 또한 많아질 수 있다.
그러나 codebase에 테스트들을 추가한다면 이를 예방할 수 있다.
Test suite의 주 목적은 코드의 변경사항을 web application으로 deploy 하기 전에 에러를 잡아내는 것이다.

그러나, test suite를 작성하는데 주의를 기울이지 않는다면, 불필요한 test code들이 늘어나 결과적으로 test suite들이 비효율적이게 될 수 있다.
따라서, full-stack web app을 개발할 때에는 작성하는 test suite들의 필요성을 신중해 고민할 필요가 있다.

## Layers in full-stack web applications

Full-stack web app은 크게 3가지 layer로 구분할 수 있다.

- User의 browser에 나타나는 **View**
- HTTP Request를 처리하는 **Server**
- User의 interaction 정보를 저장하는 **Database**

예를 들어 게시글에 comment를 달 수 있는 feature를 추가한다고 하면,

 - Browser가 게시글 아래에 comment를 rendering 할 수 있는지
 - User가 textarea안에 글을 작성하고 submit button을 누르면, comment를 post할 수 있는지
 - Server가 comment 내용을 전달 받을 수 있는지
 - Server에서 POST Request의 에러가 없는지 확인하고, 없으면 database에 comment를 잘 저장할 수 있는지
 - 새로 들어온 User가 최신의 comment를 commnet list 최상단에서 볼 수 있는지

 의 여부를 test 해야 한다.

## Integration Tests vs Unit Tests

 앞서 다뤘듯이 full-stack web app은 서로 다른 layer들로 구성된다.
 각 layer들은 그 아래에 있는 layer와 상호작용을 하여 영향을 받는다.

 **Unit test**는 web-app의 작은 behavior들을 확인하며 서로 독립되어 있고 상대적을 빠르다.
 예를 들어, database가 comment를 정상적으로 저장할 수 있는지 확인하는 test는 unit test라고 할 수 있다.

 **System test**는 완전히 integrated된 test로 전체 web-app이 톱니바퀴 물리듯 잘 동작하는지를 test한다.
 예를 들어, database가 comment를 정상적으로 저장하는지, server가 browser로 HTML을 정상적으로 보내는지, browser가 view를 정상적으로 rendering하는지 모두를 검사한다.
당연하게도 모든 부분을 test하다보니, unit test에 비해 시간이 오래걸리게 된다. 
그러나 전체 시스템이 설계한 대로 잘 동작하는지 한 눈에 알 수 있다는 장점이 있다.

**Integration test**는 Unit test와 System test의 중간에 있다고 볼 수 있다.
web-app의 multiple layer를 test하며 System test보다는 빠르지만, Unit test보다는 느리다.

따라서, 이상적인 full-stack web application의 testin suite는 전체 application이 정상적으로 동작하는지 확인할 수 있어야 하며, 적은 integration test와 다수의 unit test로 구성하여 빠르게 개발자에게 feedback을 줄 수 있어야 한다.

## The Testing Pyramid

![](https://s3.amazonaws.com/codecademy-content/programs/tdd-js/articles/testing-pyramid.jpg)

Browser level의 inregration test의 수를 적게 유지하는 것이 좋다.
이는 browser-level의 test가 다른 level의 test들 보다 시간이 오래걸리기 때문이다.

Server test는 browser layer보다는 model 또는 database layer와 상호작용한다.
Browser test보다는 시간이 덜 걸리지만 Database test보다는 시간이 더 걸린다.

Database test는 위의 두 level의 test들에 비해 빠르지만 전체 시스템이 잘 작동하는지 insight를 주기에는 부족함이 있다.
이 layer에 unit test를 추가하는 것은 time cost가 적기 때문에 많은 test를 추가해도 총 test시간에 큰 영향을 미치지는 않는다.

## Conclusion

위에서 얘기했듯이, full-stack web-app을 개발하면서 test suite을 작성할 떄에는 어떻게 optimize할 수 있을지 치열하게 고민해야 한다.
Test suite을 작성하기 전에 스스로 아래왁 같은 질문들을 던져보면 도움이 될 거라고 생각한다.

- Feature level의 integration test가 필요한가?
- 같은 behavior를 server, model layer test로 test 할 수 있는가
- Server. model layer tests 들을 통해 전체 web-app의 무결성에 대해 얼마나 신뢰도를 가질 수 있는가
- 이 feature test를 완료하는데 어느 정도 시간이 걸리는가


