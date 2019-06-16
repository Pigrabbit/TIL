# Shortcuts for moving cursor in vim 

terminal에서 vim editor를 이용하면서 cursor를 움직임에 있어 미숙한 점이 많았다.
기본 h, j, k, l의 네 가지만 이용해서 움직이기에는 작업 효율이 떨어졌다고 느꼈기 때문에 다른 방법이 없는지 찾아보게 되었다.

## Vertical move

- gg: 문서 맨 위로
- H: 현재 페이지 맨 위 line으로
- ctrl + b: 한 페이지 위로 
- ctrl + u: 반 페이지 위로
- ctrl + g: cursor는 그대로 두고 화면만 1 line씩 위로 scroll
- k: 한 줄 위로
- M: 현재 페이지 중간 line으로
- j: 한 줄 아래로
- ctrl + e: cursor는 그대로 두고 화면만 1 line씩 아래로 scroll
- ctrl + d: 반 페이지 아래로
- ctrl + f: 한 페이지 아래로
- L: 현재 페이지 맨 아래 line으로
- G: 문서 맨 아래로
- number + gg or G: 해당 number의 line으로 이동

## Horizontal move

- ^: line 맨 앞으로
- ge: 한 단어 (공백을 기준으로 함) 왼쪽으로 이동해 cursor를 단어 가장 오른쪽에
- b: 한 단어 (공백을 기준으로 함) 왼쪽으로 이동해 cursor를 단어 가장 왼쪽에
- h: 한 칸 왼쪽으로
- l: 한 칸 오른쪽으로
- w: 한 단어 오른쪽으로 이동해 cursor를 단어 가장 왼쪽에
- e: 한 단어 오른쪽으로 이동해 cursor를 단어 가장 오른쪽에
- $: line 맨 끝으로

## Find

- F + ?: 왼쪽 방향으로 검색하며 찾으려고 하는 문자(?)이전으로 cursor 이동
- T + ?: 왼쪽 방향으로 검색하며 찾으려고 하는 문자(?)다음으로 cursor 이동
- f + ?: 오른쪽 방향으로 검색하며 찾으려고 하는 문자(?)다음으로 cursor 이동
- t + ?: 오른쪽 방향으로 검색하며 찾으려고 하는 문자(?)이전으로 cursor 이동

