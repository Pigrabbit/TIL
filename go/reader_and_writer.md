# Reader and Writer in Golang

byte array를 읽어 Decode 하는 작업에서 misunderstand 한 내용을 정리

## Reader
Reader 는 기본적인 Read method를 감싸주는 인터페이스이다.

Read 메소드는 parameter로 받은 byte slice의 길이만큼까지 읽을 수 있다.
읽은 후에 실제로 읽은 byte 길이(integer)와 에러가 있다면 에러를 리턴한다.

n(>0)개의 byte를 읽은 후 error 또는 EOF 상황에 놓이게 되면 Read()는 읽은 byte 수인 n을 리턴한다.

Caller는 에러를 고려하기 전에 0보다 n을 처리해야한다.
이렇게 하면 어떤 byte를 읽은 뒤에 발생하는 I/O error와 EOF를 처리할 수 있다.

Read()는 읽은 바이트 수(n)=0, nil 에러를 동시에 리턴하도록 구현되지 않았다.
(input byte slice의 길이가 0인 경우 예외)
이 때문에 0과 nil을 받았다면 아무일도 벌어지지 않은것이지 EOF가 아님을 숙지해야 한다.
특별히 EOF를 나타내지 않는다.

``` go
type Reader interface {
	Read(p []byte) (n int, err error)
}
```

## Writer

Write()는 parameter로 받은 byte slice p의 길이 만큼을 데이터 스트림에 쓴다.
0 <= n <= len (p)의 적은 바이트 수 및 writer를 일찍 멈추게 한 원인이 된 에러를 돌려준다. 
n < len (p)이면 nil이 아닌 오류를 반환해야한다. 
또한 일시적으로라도 슬라이스 데이터를 절대 수정해서는 안된다.


```go
type Writer interface {
	Write(p []byte) (n int, err error)
}
```

[Reference](https://golang.org/pkg/io/#Reader)

[Streaming IO in Go](https://medium.com/learning-the-go-programming-language/streaming-io-in-go-d93507931185)
