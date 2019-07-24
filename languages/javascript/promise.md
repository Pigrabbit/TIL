# What is a Promise?

Promises are objects that represent the eventual outcome of an asynchronous operation. A Promise object can be in one of three states:
Promise 는 asynchronous 작업 후 결과를 나타내는 object이며 3 가지 상태가 있다.

- **Pending**: 초기 상태로 async 작업이 완료되지 않은 상태이다.
- **Fulfilled**: Async 작업이 완료되었으며 promise는 resolved value를 가지고 있다(JSON 형태로).
- **Rejected**: Async 작업이 실패한 상태로 실패한 이유를 가지고 있다.

Promise가 더 이상 pending이 아닐 때 이 것이 settle 되었다고 한다. 그 상태는 fulfilled 일 수도 rejected 일 수도 있다.

우리 주변에서 예를 찾아본다면, 식기세척기의 경우

- **Pending**: 세척기를 돌리기 전 상태
- **Fulfilled**: 세척을 완료해 접시들이 깨끗해진 상태
- **Rejected**: 세척이 정상적으로 완료되지 못한 상태

라고 설명할 수 있겠다.

## Chaining Multiple Promises

Async 방식으로 프로그래밍할 때 가장 흔한 패턴은 서로 의존적인 작업들을 원하는 순서로 실행시키는 것이다.
예를 들어 database에 request를 보내고 return된 data를 바탕으로 request를 보내는 경우가 있을 것이다.

우리가 세탁을 하는 과정을 async 방식으로 이해해보자.

먼저 세탁할 옷들을 세탁기에 넣고 세탁기를 작동시킨다.
옷이 깨끗하게 세탁되었다면, 이를 건조기에 넣고 돌린다.
건조기 동작이 끝났을 때, 옷들이 잘 말랐다면 그것들을 잘 개서 보관한다.

직접 javascript 코드를 살펴보자.

``` javascript
firstPromiseFunction()
.then((firstResolveVal) => {
  return secondPromiseFunction(firstResolveVal);
})
.then((secondResolveVal) => {
  console.log(secondResolveVal);
});
```

- 먼저 `firstPromiseFunction()`을 호출하고 `.then()`으로 anonymous 함수를 chaining 한다.
- `then()`의 success handler 에서 새로운 promise를 return 한다. 이 promise는 `secondPromiseFunction()`을 첫 promise의return value로 호출한 결과다.
- 그 다음 두 번째 `then()`을 호출해 second promise 의 settlement를 처리한다.

## Common mistakes to avoid

Promise의 가장 큰 장점은 nested 된 callback(일명 callback 지옥)에서 벗어날 수 있다는 점이다.
그러나, Promise와 handler를 이용하다보면 몇가지 실수를 쉽게 범할 수 있다.

첫번째는 promise들을 chaining하지 않고 nesting 하는 것이다.

```javascript
returnsFirstPromise()
 .then((firstResolveVal) => {
	return returnsSecoundValue(fristResolveVal)
   	  .then((secondResolveVal) => {
        console.log(secondResolveVal)
	  })
  })
```

원하는 대로 코드가 작동하기는 하겠지만 지금 2개인 promise가 10개 또는 그 이상이 된다면 상상만해도 그 코드는 머리가 아플 것이다.

두번째는 promise를 return하지 않는 실수이다.

```javascript
returnsFirstPromise()
  .then((firstResolveVal) => {
     returnsSecondValue(firstResolveVal)
  })
  .then((someVal) => {
    console.log(someVal);
  })
```

이 때 두 번쨰 `.then()`에서 처리하는 `someVal`은 두 번째 promise의 settled value가 아니라 첫첫 번째(returnsFirstPromise) promise의 settled value이다.
따라서 에상하던 결과와 다른 값이 콘솔에 출력되는 것을 확인할 수 있다.

## When you want to getting things done asynchronously

`Promise.all()`을 이용하면 서로 독립된 여러 작업들을 async하게 수행할 수 있다.
promise들의 array를 argument로 받아 하나의 promise를 return 한다.
결과 promise는 다음 둘 중 하나로 settle하게 된다.

- array의 모든 promise들이 resolved 됐다면 그 promise들의 resolved value를 element로 가진 array를 return 한다.
- array의 어떤 하나의 promise라도 rejected 됐다면 rejected 된 이유와 함께 그 즉시 reject 된다.

직접 javascript 코드를 살펴보자.

``` javascript
let myPromises = Promise.all([returnsPromOne(), returnsPromTwo(), returnsPromThree()]);

myPromises
  .then((arrayOfValues) => {
    console.log(arrayOfValues);
  })
  .catch((rejectionReason) => {
    console.log(rejectionReason);
  });
```

- `Promise.all()`을 3 개의 promise를 가진 array를 pass하여 호출한다.
- 성공한 경우(resolved),  `then()`안의 내용이 실행된다. 이 경우 resolved value들의 array를 출력한다.
- 실패한 경우(rejected), `catch()`안의 내용이 실행된다. 이 경우 first rejection message를 출력한다.

