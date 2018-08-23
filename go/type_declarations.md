# Type Declarations

 go에서의 [type declaration](https://golang.org/ref/spec#Type_declarations) 에는 **Alias declarations** 와 **Type definitions**의 2 가지 형태가 있다.
 

### Alias declarations

Type alias는 기존에 있던 type에 새로운 이름을 붙여주는 일이다.  
일반적으로 이해하기 쉬운 코드를 위해 짧은 이름이나 의미있는 이름을 붙여준다.

```go  
type celsius float64  
type temperature = celsius  
```

**=** 양쪽에 있는 temperature와 celsius의 type은 identical 하다.


### Type definitions

type definition은 새로운 구별되는(전에 없던) type을 만들어주는 일이다.  
위의 예에서 `celsius`는 `float64`와 다른 type이 된다.

여기서 중요한 것은 **methods**인데 Alias한 type의 경우 기존에 있던 type의 method를 그대로 사용가능하다.  
그러나, 새로 define한 type의 경우에는 기존에 있던 type의 method를 사용할 수 없다. 

```go  
type struct Person{  
    name   string  
    age       int  
}  
func (p *Person) Eat() {  /* do something */ }  
func (p *Person) Run() { /* do something */ }  
type athlete Person  

```

`athlete` type은 Person의 properties인 `name`, `age`를 그대로 갖게 되지만,  
method인 `Eat()`, `Run()`등은 상속받지는 않는다.  
이 methods 를 사용하고 싶다면
`Person(athlete)` 의 형태로  **type conversion**이 필요하다.

