# What is Express?

Express는 웹서버나 API를 개발에 아주 유용한 Javascript framework 이다.

# Starting a server

Express는 Node 모듈으로 이것을 사용하기 위해서는 파일에서 import 해줘야 한다.
Server를 만들기 위해서 import된 express function을 invoke해줘야 한다.

``` javascript
// Import the express library
const express = require('express');
// Instantiate the application
const app = express();
```

기본적으로 server는 port를 바라보고 있으면서 들어오는 request에 대한 response를 돌려준다.
Server가 이렇게 동작하게 하기위해서 먼저 어떤 port를 listen 해야되는지 `app.listen()`에 argument로 넘겨줘야 한다.

``` javascript
const PORT = 80;
app.listen(PORT, () => {
  console.log(`Server is listening on port ${PORT}`);
});
```

위의 Javascript 코드는 `Server is listening on port 80`란 메세지를 콘솔에 출력한다.

# Writing Route

Server가 request에 따라 어떻게 response를 보낼지 정의하기 위해 route들을 등록해주어야 한다.
Route에서 request의 path와 HTTP method에 따른 로직을 정의한다.

예를들어, server가 '/tea'의 GET request를 받았다고 하자.
Path('/tea')와 HTTP method(GET)를 이용해 route에서 적절한 로직을 구현하면 된다.

## GET

GET request는 server로 부터 resource를 가져올 때 사용한다.
Express에서는 `.get()`을 이용해 GET request에 대한 route를 register한다.
2개의 argument를 pass하는데 첫번째는 path,  두번째는 request를 다루고 response를 보내는 callback function이다.

## PUT

PUT request는 존재하는 resource를 update할 때 사용한다.
이를 위해(원하는 target resource를 update하기 위해) unique identifier를 route parameter로 포함시켜야 한다.

PUT request는 존재하는 data를 어떻게(어떤 값으로) update시켜야 하는지에 대한 정보가 필요하다.
URL의 끝부분을 유심히 살펴보면 '?'뒤로 Query string이 있는 것을 확인할 수 있다.
이 Query String은 route path로 count되지는 않는다.
대신에 Express 는 이를 parse해서 object로 만든 뒤 requst body에 `req.query`의 형태로 붙인다.

## POST

POST request는 새로운 resource를 만들 때 사용된다.
새로운 data를 생성하는 것이기 때문에, path 끝에 route parameter를 포함하진 않는다.
그러나 어떤 종류의 resource를 생성했는지 type을 path 끝에 넣는다.
Express 는 `.post()`를 이용해 POST request를 처리한다.

## DELETE

DELETE request는 존재하는 resource를 삭제할 때 사용한다.
이미 존재하는 data를 삭제하는 것이므로 path에 delete할 target resource에 대한 route parameter를 path 마지막에 넣는다.

# Sending a response

HTTP는 기본적으로 하나의 request에 대해 하나의 response를 보낸다.
Client는 하나의 request에 대해 하나의 response가 올 것이라는 것을 알고 있으며, server는 client에게 하나의 request에 대해서는 하나의 response만을 보내야 한다.

Express는 response object의 `.send()`로 response를 보낸다.
어떤 것도 input으로 받을 수 있고 그것을 response body에 포함시킨다.

# Setting Status Codes

Express에서는 res object의 `.status()` method를 통해 http status code를 보낼 수 있다.
이 response code는 client에게 그들의 request 가 어떻게 처리되었는지 정보를 준다.
http status code에 대한 정보는 [여기](https://github.com/Pigrabbit/TIL/blob/master/etc/http_status.md)

```javascript
const sweetInventory = { Sneakers: 4, Haribo: 1, Kisses: 3, Reese: 2 };
app.get('/sweet-inventory/:name', (req, res, next) => {
  const sweetInventory = sweetInventory[req.params.name];
  if (sweetInventory) {
    res.send(sweetInventory);
  } else {
    res.status(404).send('Sweet not found');
  }
});
```

위의 코드에서 `sweetInventory`에 request에서 보낸 element가 있으면 value를 전송하지만 없으면 404코드와 함께 `Sweet not found`라는 에러 메세지를 돌려준다.
