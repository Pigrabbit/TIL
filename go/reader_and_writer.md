# Reader and Writer in Golang

byte array를 읽어 Decode 하는 작업에서 misunderstand 한 내용을 정리

## Reader

`io.Reader` 인터페이스로 나타나는 reader는 source로 부터 데이터를 읽어 *transfer buffer*에 넣는다.
transfer buffer 에 있는 데이터는 streamed 되거나 consumed 될 수 있다.

``` go
type Reader interface {
	Read(p []byte) (n int, err error)
}
```

`Read()` 메소드는 읽은 byte 수 n 과 에러를 return 한다.

## Writer

`io.Writer` 인터페이스로 나타나는 writer는 buffer로 부터 데이터를 stream 하고 target이 되는 resource에 write한다.

```go
type Writer interface {
	Write(p []byte) (n int, err error)
}
```

`Write()` 메소드는 읽은 만큼의 byte 수와 에러를 return 한다.

[Reference](https://golang.org/pkg/io/#Reader)

[Streaming IO in Go](https://medium.com/learning-the-go-programming-language/streaming-io-in-go-d93507931185)
