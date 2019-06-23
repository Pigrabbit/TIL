# HTTP status codes

Status code 란 Client가 server에 보낸 request 에 대한 server의 응답이다.
Code의 가장 첫 자리는 그것이 response의 다섯가지 분류 중 어느 것인지 알려준다.

- 1xx (Informational): Request를 잘 받았으며 process를 계속 진행한다.
- 2xx (Successful): Request를 성공적으로 잘 받았고 이해했으며 accept 되었다.
- 3xx (Redirection): Request를 완료하기 위해서 추가적인 action이 필요하다.
- 4xx (Client Error): Request에 syntax 오류가 있거나 다른 이유로 인해 처리할 수 없다.
- 5xx (Server Error): Request는 Valid 했으나 server 측 오류로 정상적으로 처리하지 못했다.

## List of commonly used codes

수많은 code들 중에 흔히 사용하는 code 들만 간략히 정리해봤다.

**200 OK** :

문제없는 HTTP request에 대한 일반적인 response이다.
GET request의 경우 response 가 request 한 resourece를 들고 있을 것이며, POST request의 경우 response가 action에 대한 결과를 들고 있을 것이다.

**201 Created** :

Request가 처리되어  새로운 resource를 만들었다.

**202 Accepted** : 

Request가 accept되어 처리중이나 아직 처리가 완료되지는 않았다.
처리하는 도중에 issue가 생길 수도 있다.

**204 No Content** : 

Server가 request를 성공적으로 처리했으며 어떤 content도 return 하지 않는다(DELETE request의 경우).

**400 Bad Request** :  

Client error 때문에 server가 request 를 처리할 수 없다.
Client error의 예로는 request syntax error, 용량 문제 등이 있다.

**403 Forbidden** : 

Request는 valid했으나 server가 그 action을 거절함.
Request를 날린 user가 resource에 대한 permission이 없을 때 발생할 수 있다.

**404 Not Found** : 

Request한 resource를 현재 찾을 수 없다.


