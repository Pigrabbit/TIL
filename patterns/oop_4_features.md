# Four Features of OOP Languages

객체지향언어에는 다음의 4가지 특징이 있다.

- Abstraction
- Inheritance
- Encapsulation
- Polymorphism

하나씩 차례대로 알아보자.

## Abstraction

어떤 문제가 있을 때, 그것을 여러 개의 클래스와 그들 사이의 관계로 나타나는 modeling 하는 일이다.

## Inheritance

상위 클래스의 특징들을 하위 클래스가 물려받는 것.
예를 들어 Car 라는 부모클래스가 있다고 하자.
Car는 달릴 수 있다. 상속을 이용한다면 여기에 기능을 추가 할 수 있다.
짐을 많이 싣고 싶다면 수납공간이 넓은 hatch back Car를
더 빠른 속력을 내고 싶다면 Sport Car를 생성하면 된다.

이렇게 부모클래스로 부터 새로운 기능을 추가한 자식클래스를 생성하는 것을 **Specialization** 이라고 하며,
반대로 자식클래스들의 공통점을 찾아 부모클래스를 생성하는 것을 **Generalization** 이라고 한다.

한편, 상속을 이용하게 되면 코드 재사용을 반복을 줄일 수 있다.

## Encapsulation

Object는 data와 behavior들의 집합을 가지고 있으며 **Access modifier**를 통해 어떤 data를 외부에 노출시킬지 결정할 수 있다.
Access modifier 에는 Public, Private, Protected가 있으며(Java) 외부로 노출되는 것은 **public interface**이다.

*Principle of information hiding*에 의하면 호출하는 모듈(클래스 또는 subsystem)은 호출된 모듈의 내부에 대해 알 필요가 없으며 알고 싶어하지 않는다. 
이렇기 때문에 좋은 object 디자인이란 attribute와 operation의 노출을 최소화 하는 것이다.


## Polymorphism

Polymorphism의 사전적인 정의는 object가 다양한 형태를 가질 수 있는 능력이다.

- Parametric Polymorphism: Generics
- Inclusion Polymorphism: Subtyping, Subclassing and Overriding
	- Subtyping: 타입 A가 타입 B의 subtype 이라면, A의 value의 집합은 B의 subset이 된다.
		- Week = {월, 화, 수, 목, 금, 토, 일}, Weekend = {토, 일} 일때, WeekEnd ⊆ Week.
		- Mountainbike ⊆ Bicycle. 모든 Mountaionbike는 Bicycle이기 때문에 프로그램에서 Bicycle이 사용되는 곳에서 Mountainbike가 아무런 문제없이 대체할 수 있어야 한다. (*Liskov's substitution priciple*)
	- Subclassing: usage of an inheritance association 
	- Overriding: 상위 클래스에서 구현한 method를 하위 클래스에서 재구현하는 case. Override를 할 때 method가 전혀 새로운 일을 하지 않도록 유의하도록 한다.
- Ad-hoc Polymorphism: Overloading
	- Overloading: 같은 이름을 가진 method들이 서로 다른 signature(Parameter types and return type of a method)를 가진다.

### From Problem Statement to Model: Abott's heuristics

어떤 문제를 묘사할 때, objects, 속성, 연관관계를 자연어를 바탕으로 분석할 수 있다.

Part of speech | Model Component | Example 
|:-----: | :-----: | :----- | 
Proper noun | Instance | Alice 
Common noun | Class | Field officer 
Doing verb | Operation | cretes, submits, selects 
Being verb | Inheritance | Is kind of, Is one of 
Adjective, Genetive case | Attributes | Incident description 


### What is good design? 

- less Complexity: Information Hiding
- prepared for Change
- low coupling between subsystems: Delegation
- provides subsystems with high cohesion
