# Array Methods

Javascript의 array 데이터 타입에서 자주 사용할 것 같은 method 들을 정리해보았다.

- pop(), push()

> `pop()`은 array 의 맨 마지막 element를 빼서 return 한다.  
`push()` 는 array의 끝에 element를 추가할 때 사용하며 array의 새로운 길이를 return 한다. 

``` javascript  
var testArray = ["Altuve", "Bregman", "Correa", "Springer"];  
console.log(testArray.pop());  
// Springer  
// testArray = ["Altuve", "Bregman", "Correa"]

testArray.push("Valender");  
console.log(testArray[3]);  
// Valender  
// testArray = ["Altuve", "Bregman", "Correa", "Springer"]  
```

- concat(), slice()

> `concat()`은 둘 이상의 array를 join 할 때 사용한다. 기존의 array를 변경하지 않으며 새로 join한 array를 반환한다.  
`slice()`는 선택한 element 들을 array 형태로 return 한다.

``` javascript  
var testArray = ["Altuve", "Bregman", "Correa", "Springer"];  
var anotherArray = ["Gurriel", "Gattis"];  
console.log(testArray.concat(anotherArray));  
// ["Altuve", "Bregman", "Correa", "Springer", "Gurriel", "Gattis"]

console.log(testArray.slice(1, 3))  
// ["Bregman", "Correa"]  
```
 
- find(), findIndex()

> `find()` 는 function으로 주어지는 test를 통과하는 array의 첫번째 element를 return한다.  
Array내의 모든 element에 대해 test를 수행하며 
test 함수가 true가 되게하는 element가 있으면 그것을 return하고  
하나도 없으면 `undefined`를 return한다.
`findIndex()`는 `find()`와 비슷하지만 test를 통과하는 element의 `index`를 return한다.


```javascript  
var ages = [3, 10, 18, 20];

function checkAdult(age) {  
    return age >= 18;  
}

console.log(ages.find(checkAdult));   
console.log(ages.findIndex(checkAdult));  

// 18  
// 2  
```

- indexOf()

> `indexOf()` 는 array 안에 element가 있는지 찾고 그 index를 return 한다. `start` 인자를 전달하지 않으면 array의 시작부터 찾기 시작한다. array 내에 없는 경우 `-1`을 return한다.

``` javascript 
 
var testArray = ["Altuve", "Bregman", "Correa", "Springer"];    
console.log(testArray.indexOf("Bregman"));  
// 1   
```

- map()
>`map()`은 array의 모든 element에 대해 호출한 function의 결과를 새로운 array로 만들어 return한다.  
**Syntax**  
`array.map(function (currentValue, index, arr), thisValue)`

```javascript   
var numbers = [4, 9, 16, 25];  
console.log(numbers.map(Math.sqrt));  
// [2, 3, 4, 5] 
```
