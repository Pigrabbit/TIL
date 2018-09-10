# How Travis CI works

Build 할 떄 실행 시켜야 할 shell script 파일을 어디에 포함시켜야 할지 찾아보며 공부하게 되었다.

## What is CI?

Continuous Integration 이란 코드를 조금씩 빈번하게 merge하는 방식이다. 
이는 개발 마지막단계에 많은 양의 코드를 한 번에 merge하는 방식과 대조된다.
CI의 목표는 조금씩 코드를 더하고 테스트 하면서 더 견고한 소프트웨어를 만드는 것이다.

Travis CI는 CI 플랫폼으로서 자동으로 build, test를 지원하며 바로 변경한 코드에 대한 피드백을 주는 것으로  개발 단계를 도와준다.

## How does Travis CI work?

build 를 실행했을 때, Travis CI는 GitHub repository를 새로운 가상환경으로 clone 하고 그 곳에서 build하기 위한 작업들을 수행하고 테스트를 진행한다.
그 작업들 중 하나 이상이 실패하게 되면 build는 **broken** 상태가 된다.
반면에, 모든 작업들이 fail하지 않는다면, 그 build는 **passed** 상태가 되며, Travis CI는 코드를 deploy 할 수 있게 된다.

## Terms used in Travis CI
- job: repository를 가상환경으로 clone하고 거기서 compiling, testing 등 일련의 *phases*를 수행하는 자동화된 과정을 말한다. **script** phase 에 대한 return이 non zero일 때 fail한다.
- phase: job에서 수행하는 일련의 과정들. `install` -> `script` -> `deploy` phase의 순서
- build: job들의 집합. 예를 들면 서로 다른 두 버전의 프로그래밍 언어로 프로젝트를 테스트 하는 경우 build는 2개의 job을 가질 수 있다.
	[Core Concepts for Beginners](https://docs.travis-ci.com/user/for-beginners/)

## The Build Lifecycle

Travis CI의 build 는 `install`과 `script` 두 단계로 구성된다.
install 단계에서는 필요한 dependency들을 설치하며, script 단계에서는 build script를 실행한다.

원한다면 임의로 `before_install`, `before_script` 또는 `after_script` 단계를 추가 할 수 있다.
`before_install` 단계에서는 프로젝트에 필요한 Ubuntu package 등 추가적으로 dependency들을 설치 할 수 있다.

선택할 수 있는 단계를 포함한 완전한 build cycle은 아래와 같다.

1. OPTIONAL Install `apt addons`
2. OPTIONAL Install `cache components`
3. `before_install`
4. `install`
5. `before_script`
6. `script`
7. OPTIONAL `before_cache` (for cleaning up cache)
8. `after_success` or `after_failure`
9. OPTIONAL `before_deploy`
10. OPTIONAL `deploy`
11. OPTIONAL `after_deploy`
12. `after_script`

## Customizing the Installation Step

`travis.yml`에 명시하면 프로젝트에 필요한 dependency를 설치하는 직접 작성한 script(.sh)를 실행시키도록 할 수도 있다.
이 때, 스크립트가 실행가능 하도록 *chmod +x*를 사용하고 경로를 올바르게 지정해주는 것이 중요하다.

여러 단계를 실행하도록 명시할 수도 있다. 
이 때 어느 단계중에 하나가 실패하게 되면 build는 멈추고 **errored**를 나타낸다.
