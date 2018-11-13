# Basic Concept of Object Oriented Program

개발을 시작한 지 얼마 안됐더라도 객체지향, Object Oriented Program 이라는 용어를 많이 접해봤을 것이다.
본인도 얼마전까지만 해도 명확한 개념보다는 개괄적으로 알고 있었는데, 
Pattern Design을 공부하면서 복습한 내용을 정리해보려고 한다.

*"Many design and architectural patterns use a combination of inhertance and delegation."*

## Phenomena and Concepts

- Phenomenon
	- An object in the world of a domain as you perceive it
	- 인지한 어떠한 대상, object

- Concept
	- Describes the common properties of phenomena
	- Phenomena의 공통 특성에 대한 묘사 
	- A concept is a 3-tuple: Name, Purpose and members.

에를 들어 '시계'라는 Concept에 대해 얘기하자면,
'시계'가 Name, '시간을 측정하는 기구'가 Purpose, 손목시계, 모래시계, 자명종 등이 Members가 된다.

## Abstraction and Modelling

- Abstraction
	- Classification of phenomena into concepts
	- Phenomena 를 concpets로 분류하는 일

- Modeling
	- Development of abstractions to answer specific questions about a set of phenomena while ignoring irrelevant details
	- 불필요한 detatil들을 무시하면서 어떤 phenomena에 대한 구체적인 문제에 답하기 위해 absraction을 develop하는 일.

## Types and Instances

Phenomena 나 Concept 같은 용어는 철학에서 자주 사용되며 Computer Science에서는 Type, Instance라는 용어를 더 자주 사용한다.

- Type
	-  A concpet in the context of programming languages
	- 예를 들어 
		- Name: boolean
		- Purpose: logical truth values
		- Members: true, false

- Instance
	- A member of a specific type

어떤 변수의 type은 그 변수가 가질 수 있는 모든 instance를 나타낸다. 이 관계는 Object, Class 사이의 관계와 비슷하다

## Classes and Objects

- Classes
	- In object-oriented programming languages a complex type is represented by a class.
	- 객체지향 언어에서 complex type은 클래스로 나타내어 진다.
	- A class is a code template for a type, that is used to create instances of that type
	- 클래스는 type을 위한 코드 템플릿이며 그 타입의 instance를 생성하기 위해 사용된다.
	- 클래스에는 attributes와 methods가 있다.

- Objects
	- 클래스의 instance를 Object라고 한다.
