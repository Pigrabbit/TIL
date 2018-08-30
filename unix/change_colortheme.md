# Change colortheme in terminal

만약 매일 작업해야 하는 환경이 검정 바탕에 흰 글씨만 있는 터미널이라면 작업을 하고 싶다는 마음이 잘 안들것이라고 생각한다.
작업을 시작하더라도 터미널을 읽다가 금방 피곤해질 것이 분명하다.

새로 Mac을 접하면서 터미널을 자주 이용하게 되었는데 이번 기회를 통해 터미널을 내 입맛에 맞게 꾸며보았다.

```
# ANSI color codes -----------------------------------------------------------
# https://gist.github.com/chrisopedia/8754917
GREEN='\e[0;32m\]'
B_MAGENTA='\e[1;35m\]'
YELLOW='\e[0;33m\]'
RED='\e[0;31m\]'
CYAN='\e[0;36m\]'
COLOR_END='\[\033[0m\]'

# PROMPT ----------------------------------------------------------------------
TIMESTAMP='\D{%F %a %T}'
GIT_BRANCH=''
if [ $(which vcprompt 2> /dev/null) ]; then
 GIT_BRANCH="\$(vcprompt -f '[%b %r]')"
fi
PS1="${YELLOW}${TIMESTAMP} ${GREEN}\u ${RED}\h ${CYAN}\w ${COLOR_END} ${GIT_BRANCH}\n\$ "
export PS1

# coloring by row
export CLICOLOR=1

export LSCOLORS=ExFxBxDxCxegedabagacad
```

현재 본인의 터미널 세팅은 위와 같다.
color는 ANSI color code에 따라 정할 수 있다.

Reference: http://osxdaily.com/2013/02/05/improve-terminal-appearance-mac-os-x/
