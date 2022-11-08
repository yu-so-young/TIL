# Vue.js 개념

Vue.js : Front End Framework

React, Angular, Ember, Vue.js, Svelte 등이 있으나 Angular보다 Vue.js의 만족도, 관심이 높음

React가 거의 1위

# MVVM Pattern

---

`Model` + `View` + `ViewModel`

- Model: 순수 자바스크립트 객체
- View: 웹페이지의 DOM
- ViewModel: Vue 의 역할

기존에는 JavaScript에서 View에 해당하는 DOM에 접근하거나 수정하기 위해 jQuery와 같은 라이브러리 이용

Vue는 **View와 Model을 연결하고 자동으로 바인딩**하므로 **양방향 통신을 가능하게 함**

![스크린샷 2022-11-08 오후 3.11.10.png](Vue%20js%20%E1%84%80%E1%85%A2%E1%84%82%E1%85%A7%E1%86%B7%209cb17803d2b54e22a14c3f08aee9c4fe/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2022-11-08_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_3.11.10.png)

# Vue Instance

---

템플릿 렌더링부터 데이터 바인딩 등의 동작 수행

```html
<script>
	new Vue({
		el: '#app',
		data: function(){
			return {
				message: '',
			}
		},
	});
</script>
```

## Vue Instance 생성 : `new Vue({  });`

### **옵션 속성의 종류**

- `el` : Vue가 적용될 요소 지정, CSS Selector or HTML Element(id, class, tag명)
    - `el: ‘#app’` ⇒ id=”app” 인 html element
- `data` : Vue에서 사용되는 정보 저장. 객체 또는 함수의 형태
- `template` : 화면에 표시할 html, css 등의 마크업 요소를 정의하는 속성. Vue의 데이터 및 기타 속성들도 함께 화면에 그릴 수 있음
- `methods` : **화면 로직 제어**와 관계된 method를 정의하는 속성. 마우스 클릭 이벤트 처리와 같이 화면의 전반적인 이벤트와 화면 동작과 관련된 로직을 추가
    - method 안에서 data를 “this.데이터이름”으로 접근할 수 있음
- `created()` : Vue Instance가 **생성되자마자** 실행할 로직을 정의
- `computed` : getter/setter 를 지정하는 옵
- 등등

### **유효범위**

Vue Instance를 생성하면 HTML의 특정 범위 안에서만 옵션 속성들이 적용됨(el 속성과 밀접한 관계)

인스턴스가 화면에 적용되는 과정

- Vue 라이브러리 파일 로딩
- 인스턴스 객체 생성(옵션 속성 포함) : new Vue({ });
- el 속성에 지정한 화면 요소(DOM)에 인스턴스가 부착됨
- 인스턴스의 data 속성이 el 속성에 지정한 화면 요소와 그 이하 레벨의 화면 요소에 적용되어 값이 치환됨
- 변환된 화면 요소를 사용자가 최종 확인

## Life Cycle

<aside>
📌 크게 나누면 **생성**, **부착**, **갱신**, **소멸**의 4단계

**beforeCreate**

: Vue 인스턴스가 생성되고 각 정보의 설정 전에 호출. **DOM과 같은 화면요소에 접근 불가**

**created**

: Vue 인스턴스가 생성된 후 데이터들의 설정이 완료된 후 호출.

인스턴스가 화면에 부착되기 전이므로 **template 속성에 정의된 DOM 요소는 접근 불가**.

서버에 데이터를 요청(http 통신)하여 받아오는 로직을 수행하기 좋음

---

**beforeMount**

: 마운트가 시작되기 전에 호출

**mounted**

: 지정된 element에 Vue 인스턴스 데이터가 마운트 된 후에 호출.

**template 속성에 정의한 화면 요소에 접근할 수 있어** 화면 요소를 제어하는 로직 수행

---

**beforeUpdate**

: 데이터가 변경될 때 virtual DOM이 랜더링, 패치 되기 전에 호출

**updated**

: Vue에서 관리되는 데이터가 변경되어 DOM이 업데이트 된 상태.

데이터 변경 후 화면 요소 제어와 관련된 로직을 추가

---

**beforeDestroy**

: Vue 인스턴스가 제거되기 전에 호출

**destroyed**

: Vue 인스턴스가 제거된 후에 호출

</aside>

![스크린샷 2022-11-08 오후 3.41.38.png](Vue%20js%20%E1%84%80%E1%85%A2%E1%84%82%E1%85%A7%E1%86%B7%209cb17803d2b54e22a14c3f08aee9c4fe/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2022-11-08_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_3.41.38.png)

![스크린샷 2022-11-08 오후 3.41.51.png](Vue%20js%20%E1%84%80%E1%85%A2%E1%84%82%E1%85%A7%E1%86%B7%209cb17803d2b54e22a14c3f08aee9c4fe/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2022-11-08_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_3.41.51.png)

## Directive 디렉티브

---

v-접두사가 있는 특수 속성

디렉티브 속성 값은 단일 JavaScript 표현식이 됨(v-for 예외)

디렉티브의 역할은 표현식의 값이 변경될 때 사이드 이펙트를 반응적으로 DOM에 적용

`v-model`

- 양방향 바인딩 처리를 위하여 사용(form의 input, textarea)

`v-bind`

- 엘리먼트의 속성과 바인딩 처리를 위하여 사용
- 약어로 “ : “ 사용 가능

`v-show`

- 조건에 따라 엘리먼트를 화면에 렌더링
- 항상 렌더링하지만 display:none 적용됨
- template, v-else 지원하지 않음

`v-if`, `v-else-if`, `v-else`

- 조건에 따라 엘리먼트를 화면에 렌더링
- false일 경우 렌더링하지 않고 element 아예 삭제
- template, v-else 지원함

`v-for`

- 배열이나 객체의 반복에 사용
- v-for=”요소변수이름 in 배열” 혹은 v-for=”(요소변수이름, 인덱스) in 배열”
- 추가로 :key=”인덱스” 필요한 경우도 있음

`v-cloak`

- Vue 인스턴스가 준비될 때까지 mustache 바인딩을 숨기기 위하여 사용
- [v-cloak] {display: none} 과 같은 CSS 규칙과 함께 사용
- Vue 인스턴스가 준비되면 v-cloak은 제거됨
    
    ```html
    <style>
    	[v-cloak]::before {  }
    	[v-cloak] > * { display:none }
    </style>
    
    <div v-cloak>{{ message }}</div> <!-- {{ }} 숨기기 위하여 사용 -->
    ```
    

## Interpolation 보간법

Vue 인스턴스의 데이터를 DOM에 바인딩 할 수 있는 문법

---

### 문자열 - Mustache(이중 중괄호)

{{ message }}

### 텍스트보간 - ‘v-text’

v-text=”data”

### HTML보간 - ‘v-html’

텍스트 구문 안에 html 구문을 넣어서 출력 가능

v-html=”html구문 data” (data의 내용 그대로 html로 인식하여 추가하겠다)

### Attribute보간 - ‘v-bind’

v-bind:[key]=”data” (key의 값을 바인딩된 data 값으로 하겠다!)