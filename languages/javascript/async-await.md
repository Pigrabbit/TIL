# Async Await in Javascript

Callback function을 통해 비동기 처리를 하던 Javascript는 ES6 부터 Promise를 도입하여 사람들을 callback hell로 부터 구해주었다.
Promise가 기존 Callback 함수보다 가독성이 좋고 debugging이 용이헀지만 여기서 또 불편함을 느끼고 ES8에서는 Async Await이라는 새로운 방법이 도입되었다.
`.then()`을 이용해서 chaining하는 복잡한(Callback function보다는 덜 복잡한) 방법에서 벗어나 `async ... await`의 keyword 만을 이용하여 비동기 처리를 하는 멋진 방법이 우리에게 다가온 것이다.

## Advantages of using Async Await

`async... await`이 도입되면서 기존 비동기 처리를 하던 code의 길이를 눈에 띄게 줄일 수 있게 되었다.
이뿐 아니라, 코드가 synchronous 와 비슷한 모양을 가지면서 개발자들이 유지 및 debugging하기 수월해졌다.
또한, 비동기 처리를 통해 resolved된 value들을 변수에 저장하여 refer하기 편리해졌다.

## Handling Errors

Promise chaining에서 `.catch()`를 사용하여 error를 처리했다면, `async...await`에서는 `try...catch`구문을 사용한다.
이 방법을 사용하면, synchronous code와 같은 방법으로 error를 handling 할 수 있으며 synchronous, asynchronous 양쪽에서 발생하는 error를 한 번에 검출할 수 있다.

```javascript
async function usingTryCatch() {
  try {
      let resolveValue = await asyncFunction('thing that will fail');
      let secondValue = await secondAsyncFunction(resolveValue);
  } catch (err) {
      // Catches any errors in the try block
      console.log(err);
  }
}

usingTryCatch();
```

## Concurrency

`async...await` 에서도 기존의 `Promise.all()`을 이용해 동시에 여러 작업을 수행할 수 있다.

```javascript
async function asyncPromAll() {
   const resultArray = await Promise.all([asyncTask1(), asyncTask2(), asyncTask3(), asyncTask4()]);
   for (let i = 0; i<resultArray.length; i++){
     console.log(resultArray[i]); 
   }
}
```

위의 코드에서 `Promise.all()`이 resolve될 때 까지 `await`하며 `resultArray`에는 각 AsyncTask들의 resolved value가 저장된다.

이 `Promise.all()`의 또 다른 장점은 비동기 작업중에 어느 하나가 rejected 되면 그 순간 다른 작업들은 종료되고 promise를 return한다.
따라서 시간을 절약할 수 있다.
