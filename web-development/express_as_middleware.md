Express는 middleware function들의 집합이다.
Middleware function 들은 request object(req), response object(res), 다음 middleware function(next)에 accessible하다. 
어떤 middleware function에서 이 일련의 request-response cycle을 완료하지 않았다면 request가 hanging된 상태로 남게된다.
이를 막기위해 `next()`로 다음 middleware function을 call 해주어야 한다.

Express application에서는 아래와 같은 middleware 종류들을 사용할 수 있다.

- [Application-level middleware](#application-level-middleware)
- [Router-level middleware](#router-level-middleware)
- [Error-handling middleware](#error-handling-middleware)
- [Third-Party middleware](#third-party-middleware)

# Application-level middleware

app object에 binding되어있는 middleware로 `app.use()` 나 `app.METHOD()` (METHOD: GET, PUT, POST, DELETE)의 형태로 사용할 수 있다.

``` javascript
var app = express()

app.use(function (req, res, next) {
  console.log('Time:', Date.now())
  next()
})
```

`.use()`에 첫번째 인자로 path를 pass하지 않은 경우, 이 function은 매번 실행되게 된다.

``` javascript
app.get('/user/:id', function (req, res, next) {
  res.send('USER')
})
```

`.get()`의 가장 간단한 예로 '/user/:id'의 path로 타고 들어갔을 때 response를 보낸다.

``` javascript
app.get('/user/:id', function (req, res, next) {
  if (req.params.id === '0') {
	next('route')
  } else {
	next()
  }
}, function (req, res, next) {
  res.send('regular')
})

app.get('/user/:id', function (req, res, next) {
  res.send('special')
})
```

위와 같이 req object의 value들을 가지고 control flow를 짤 수 있으며, `next()`를 이용해 stack에 있는 다음 middleware function을 실행할 수 있다.

# Router-level middleware

application-level middleware와 거의 비슷하다(`router.use()`, `router.METHOD()` 등 사용방식이 같음).
중요한 차이점은 `express.Router()`는 route들만 관리하는 반면 `express()`는 application level로 server connection, routes, middleware, database connection 등 더 많은 역할을 맡고 있다는 것이다.
Router를 사용함으로써 같은 path에 대한 middleware function들을 모아서 관리할 수 있다.

``` javascript
const express = require('express');
const playersRouter = express.Router();

app.use('/players', playersRouter);

const players = [alice, bob, charlie, denny];
playersRouter.get('/:id', (req, res, next) => {
  const player = players[req.params.id];
  if (player) {
	res.send(player);
  } else {
	res.status(404).send();
  }
}
```

위와 같이 코드를 작성하면 `playersRouter`에서 '/players'가 path에 prepend 되도록 해서, 그 path로 들어오는 request를 `playersRouter.get()`에서 처리하도록 한다.

# Error-handling middleware

Error-handling middleware function을 작성할 때는 항상 4 개의 arguments를 pass하도록 한다.

``` javascript
app.use(function (err, req, res, next) {
  console.error(err.stack)
  res.status(500).send('Something broke!')
})
```

# Third-party middleware

다음과 같은 방식으로 Third-party middleware를 사용할 수 있다.

``` javascript
var express = require('express')
var app = express()
var cookieParser = require('cookie-parser')

// load the cookie-parsing middleware
app.use(cookieParser())
```

Express에서 사용가능한 third-party middleware는 다음 [목록](https://expressjs.com/en/resources/middleware.html)에.

Reference: [Express 가이드 문서](https://expressjs.com/en/guide/using-middleware.html#middleware.application)

