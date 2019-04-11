pyenv: Python 버전 관리 툴
==================================
* **프로젝트마다 다른 버전** 의 Python 사용가능
* 버전별로 command를 검색할 수 있다



## Installation

	1. pyenv를 설치할 경로를 확인 한다. `$HOME/.pyenv` 를 추천하지만 어디에 설치해도 상관 없다.
		`$ git clone https://github.com/pyenv/pyenv.git ~/.pyenv`

	2. `__PYENV_ROOT__` 에 환경변수를 설정한다.
		```bash
		$ echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bash_profile
		$ echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bash_profile
		```

	3. shell 에 `pyenv init` 을 입력한다.

	4. shell을 다시 시작하여 path가 변경된 것을 적용시킨다.

	5. Python version을 `$(pyenv root)/versions` 에 설치한다. Python 3.6.5 를 설치하고 싶다면,
		```bash
		pyenv install 3.6.5
		```


### Homvbew on Mac OS X
		
	Mac OS X에Homebrew package manager 이용해서 설치도 가능하다.
		``` bash
		$ brew update
		$ brew install pyenv
		```
		

## 설치된 python 버전들 확인
	``` bash
	$ pyenv versions
	```


## 명령어가 궁금할 떄는
	``` bash
	$ pyenv help
	```


![Alt text](https://raw.githubusercontent.com/pyenv/pyenv/master/terminal_output.png)
