# Regular Experession

Regular expressions는 string에서 특정 character pattern을 나타내기 위해 사용한다.
많은 text editor와 프로그래밍 언어에서 string에서 search 및 replace를 위해 지원하고 있다.
이 때문에 regex를 알고 있는 것과 그렇지 않은 것은 프로그래밍을 할 때 큰 차이가 있다.

`/`으로 regex의 시작과 끝을 나타낸다.

`( )` 으로 일련의 pattern을 하나로 묶는다

`[ ]` 으로 가능한 문자열의 집합과 일치시킨다.
예를 들어 `[0-9]`의 regex는 숫자를 찾는다.
한편 `[ ]`안의 `^`는 not 처럼 쓰이며 `[^0-9]`는 지정한 문자(0부터 9까지의 숫자)가 없으면 매치된다.

## Reference

[wiki](https://ko.wikipedia.org/wiki/%EC%A0%95%EA%B7%9C_%ED%91%9C%ED%98%84%EC%8B%9D)

[zeta wiki](https://zetawiki.com/wiki/%EC%A0%95%EA%B7%9C_%ED%91%9C%ED%98%84%EC%8B%9D)

[javascript docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions)

