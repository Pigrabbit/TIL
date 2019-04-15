# Why do we need Vue.js?

Modern web site들은 점점 복잡하고 다양한 기능들을 수행하게 되었다.
기능이 다양해지고 web application이 복잡해지면서 아래와 같은 issue들이 생기기 시작했다.

- Code를 작성하는데 시간이 오래걸린다.
- 유지하기 어렵다. 
- 최적화하기 어렵다.(User가 사용하는데 있어)

이런 상황에서 구세주처럼 등장한 것이 Front-End Framework이다.
(Javascript의 경우 AngularJS, React, 그리고 Vue.js가 있다.)
이들은 Javascript Library로서 위의 issue들을 해결하는 데 큰 도움이 된다.
일반적인 feature들을 구현하고 Front-End code를 optimize할 수 있도록 shortcut들을 제공하기 때문이다.
정리하자면 이들은,

- Quicker to Write
- Easier to Update
- Speedy(for Users)

을 가능하게 함으로써 Front-End 개발을 더 쉽게 만드는데 기여한다.

오늘은 아래 순서로 vue.js frontend framework가 어떤 친구인지 알아보도록 하겠다.

- [Add framework to project](#add-framework-to-project)
- [Creating new Vue app](#creating-new-vue-app)
- [Vue data](#vue-data)
- [Vue forms](#vue-forms)
- [Styling with Vue](#styling-with-vue)

# Add framework to project

HTML의 `<head>`태그 안에 `<script>`태그를 추가한다.

``` html
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js" defer></script>
```

# Creating new Vue app

``` javascript
const app = new Vue({
	// the Vue constructor takes in only one object, called the options object.		
	// Each piece of information the Vue app needs to function is added to the options object as a key-value pair.
});
```

``` javascript
const app = new Vue({
  el: '#app'
  // ...
});
```

`el` key에 대한 value를 명시함으로써 HTML 파일안에 어떤 element가 vue app의 target이 될 것인지 정할 수 있다.
위의 코드에서는 id가 app인 element 가 vue app의 target이 된다.

Front-End framework라면 rendering과 dynamic data updating은 꼭 갖추어야할 기능이다.
Dynamic data를 쉽게 보여줄 수 있어야 하며 user가 그 data를 update했을 때, 즉시 update 할 수 있어야 한다.
option object 안에 `data`란 key로 data들을 관리할 수 있다. (실제 서비스를 개발할 때에는 대부분 데이터는 db로부터 가져오겠지만)

예시를 통해 `data`에 들어있는 값들을 어떻게 활용할 수 있는지 알아보자.

``` javascript
const app = new Vue({
  el: '#app',
  data: {
    username: 'Pigrabbit'
  }
});
```
	
``` html
<div id="app">
  <h2>Hello, {{ username }}</h2>
</div>
```

위와 같은 HTML 코드를 template이라고 부른다.
Template은 dynamic data들을 포함시켜 hard coding된 정보를 화면에 뿌린다.

Vue에는 Directive라고 하는 재밌는 기능이 있다.
Vue의 built-in custom attribute들로, 복잡하고 자주 사용되는 front-end 작업들을 얼마 안되는 코드로 가능하게 해준다.
덕분에 아래와 같은 것들을 할 수 있게 되었다!

``` html
<button v-if="userIsLoggedIn">Log Out</button>
<button v-if="!userIsLoggedIn">Log In</button>
```

`userIsLoggedIn`의 boolean 값에 따라 어떤 버튼을 보여 줄지 결정할 수 있으며,

``` html
<ul>
  <li v-for="todo in todoList">{{ todo }}</li>
</ul>
```

iteration을 통해 원하는 unordered list를 만들어 보여줄 수도 있다.
이외에도 많은 directive들이 있으며 [여기](https://vuejs.org/v2/api/#Directives)에서 확인할 수 있다.

Vue에서는 component를 통해 custom, reusable한 HTML element를 만들 수 있다.
Component를 만들 떄는, 이것이 HTML에서 사용되었을 때 render 될 수 있게 `template`을 명시해 주어야 한다.
또한 `props` 로 template에 채울 dynamic information들을 관리할 수 있다.

``` javascript
const Tweet = Vue.component('tweet', {
 props: ['message', 'author'],
 template: '<div class="tweet"><h3>{{ author }}</h3><p>{{ message }}</p></div>'
});
```

# Vue data

어떤 data들은 이미 들고있는 information을 바탕으로 compute된다.
이것들은 data object에 key-value 형식으로 저장될 필요는 없다.
대신에 `computed` object로 별도로 관리하며 computed object의 key는 property의 이름으로, value는 compute하는 function으로 한다.

``` javascript
const app = new Vue({
  el: '#app',
  data: {
    hoursStudied: 274
  },
  computed: {
    languageLevel: function() {
      if (this.hoursStudied < 100) {
        return 'Beginner';
      } else if (this.hoursStudied < 1000) {
        return 'Intermediate';
      } else {
        return 'Expert';
      }
    }
  }
});
```

``` html
<div id="app">
  <p>You have studied for {{ hoursStudied }} hours. You have {{ languageLevel }}-level mastery.</p>
</div>
```

Data object를 통해 computed value를 연산할 뿐 아니라 반대로 computed value를 통해 data object의 value를 update하는 것도 Vue에서 가능하다!

Computed value는 getter function안에 dynamic value가 변경되어야 recompute 된다.
그러나 computed function을 쓰지 않고 app을 update하고 싶을 때는 watch property를 사용하면 된다.
watch property의 value는 지켜보고 있어야 할 property들을 들고있는 object이다.
이 object안에 key들은 지켜보고 있어야 할 property들의 name이고, value들은 그 property가 변경되었을 때 실행되어야 할 function들이다.
아래의 코드에서 watch property는 `currentLanguage=>function() {...}` 의 key-value를 가지고 있는 object를 value로 들고 있다.

``` javascript
const app = new Vue({
  el: '#app',
  data: {
    currentLanguage: 'Javascript',
    supportedLanguages: ['Javascript', 'Python', 'Ruby'],
    hoursStudied: 193
  },
  watch: {
    currentLanguage: function (newCurrentLanguage, oldCurrentLanguage) {
		// ....
  }
});
```

Watch가 굉장히 편리해보이지만 computed value를 보다 효율적으로 update하기 위해서는 watch보단 compute를 사용하라고 Vue에서는 권장하고 있다.

Data 뿐만 아니라 Vue app에서 사용할 method들도 Vue object안에 정의할 수 있다.

``` javascript
const app = new Vue({
  el: "#app",
  data: {
    hoursStudied: 300
  },
  methods: {
    resetProgress: function () {
      this.hoursStudied = 0;
    }
  }
});
```

``` html
<button v-on:click="resetProgress">Reset Progress</button>
```

# Vue forms

위 장에서 다룬 dynamic data와 method들을 HTML 폼에서 어떻게 사용할 수 있는지 알아보자.

`v-model`을 사용하면 form field와 dynamic data를 binding할 수 있다.
form이 dynamic value와 binding되면 form에서의 값이 바뀔 때마다 Vue app에서의 값이 바뀌게 된다.
그 반대도 마찬가지로, Vue app에서 값이 바뀌면 user가 보고있는 화면의 값(form의 값) 또한 변경된다.
HTML의 text, textarea, select, radio button, checkbox등 다양한 input form들 모두 binding 가능하다.

`v-on` directive를 이용해 element에 event handler를 추가할 수 있다. 
Event handler는 특정 event에 반응해 정의된 method를 실행한다.

``` javascript
<form v-on:reset="resetForm">
  ...
  <button type="reset">Reset</button>
</form>
```

Modifer를 사용하면 directive에 기본적인 front-end logic들을 추가할 수 있다.
[list of available modifiers](https://vuejs.org/v2/api/#v-on)

Form validation은 필수 information을 user가 정확하게 입력했는지 검증하는 process이다.
아래 코드와 같이 submit button에 `v-bind` directive로 form이 valid할 때만 제출 가능하도록 구현할 수 있다.

``` javascript
const app = new Vue({ 
  el: '#app', 
  computed: { 
    formIsValid: function() { ... } 
  }
});
```

``` html
<button type="submit" v-bind:disabled="!formIsValid">Submit</button>
```

# Styling with Vue

지금까지 어떻게 dynamic web page 를 만들 수 있는지 알아보았다.
이제는 이런 dynamic한 page에 어떻게 CSS를 씌울 수 있는지 고민해 볼 차례이다.

정적인 페이지를 그릴 때, HTML파일과 CSS stylesheet source를 분리하는 것이 일반적이다.(inline styling을 적용했을 때 css코드 관리가 어렵기 때문)
그러나 front-end framework 는 이런 inline styling에 새로운 생명을 불어 넣어주었다.
CSS 코드를 concise하고 reusable하도록 지원해주었기 때문이다.

dynamic inline styling의 일반적인 패턴은 style object를 Vue app property(data 또는 computed에)로 추가하는 것이다.

``` html
<button type="submit" v-bind:disabled="!formIsValid" v-bind:style="submitButtonStyles">Confirm</button>
```

``` javascript
submitButtonStyles: function() {
  if (this.formIsValid) {
    return {
	  'background-color': '#4c7ef3',
	  cursor: 'pointer'
	}
  } else {
	return {
	  'background-color': 'gray',
	  cursor: 'default'
	}
  }
}
```

한편, inline style말고 CSS class를 적용시키는 방법도 있다.
`v-bind:class`를 이용해 CSS class를 추가할 수 있는데, 이것은 object를 value로 받는다.
value로 받는 object의 key는 class의 name이며 value는 Vue app property들 중에 하나로 true/false를 return한다.

``` css
button.active {
  cursor: pointer;
  background-color: #4c7ef3;
}
```

``` javascript
formIsValid: function() {
  return this.firstName && this.lastName && this.email && this.purchaseAgreementSigned;
}
```

``` html
<button type="submit" v-bind:disabled="!formIsValid" v-bind:class="{ active: formIsValid }">Confirm</button>
```

위의 코드는 user가 valid한 form을 작성했을 때 html의 button element가 `button.active` class에 정의한 style대로 바뀌는 예제이다.

## 짧은 소감

이상으로 Vue.js front-end framework에 대해 간단하게 알아보았다.
Dynamic data들을 front-end에서 관리하고 보여줄 뿐만 아니라, 동적으로 styling 하는 것까지 Vue가 front-end 개발을 얼마나 편리하게 해주는지 알게되었다.
MEVN Full stack을 구성하는데 한 걸음 앞으로 나아간 것 같아 기쁘다!
