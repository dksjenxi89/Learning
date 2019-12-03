[Do it! vue.js - 장기효] {http://www.yes24.com/Product/Goods/58206961?Acode=101}

## 화면을 개발하기 위한 필수 단위 - 인스턴스 & 컴포넌트

왜 UI를 설계할 땐 컴포넌트가 필요하고, 화면을 그리기 위해서는 인스턴스가 있어야 할까?

### 뷰 인스턴스
뷰 인스턴스는 뷰로 화면을 개발하기 위해 필수적으로 생성해야 하는 기본 단위이다.

뷰 인스턴스를 생성해보자!

#### 뷰 인스턴스 형식
~~~vue

new Vue ({
  ...
});

~~~
new Vue()로 인스턴스를 생성할 땐 Vue 생성자라고 부른다. JS와 같다!

### 생정자 정리!
생정자는 객체를 새로 생성할 때 자주 사용되는 옵션과 기능들을 미리 특정 객체에 저장해 놓고,
새로 객체를 생성할 때 기존에 포함 된 기능과 더불어 기존 기능을 쉽게 확장하여 사용하는 기법이다.
일반적으로 객체 지향 프로그래밍에서 사용하는 객체 정의 방식으로 미리 정의 된 속성과 메서드를 재활용하기 위해 사용한다.


![image](https://user-images.githubusercontent.com/57930450/69201962-6ae16880-0b83-11ea-93dc-a8b3ff491a63.png)

인스턴스 안의 :으로 작성 된 부분은 속성이라고 한다.
각각 el 속성, data 속성

### 뷰 인스턴스 옵션 속성
뷰 인스턴스 옵션 속성은 인스턴스를 생성할 때 재정의할 data, el, template 등의 속성을 의미한다.

### template : 화면에 표시할 HTML, CSS등의 마크업 요소를 정의하는 속성, 뷰의 데이터 및 기타 속성들도 함께 화면에 그릴 수 있다.
### methods : 화면 로직 제어와 관계 된 메서드를 정의하는 속성, 마우스 클릭 이벤트 처리와 같이 화면의 전반적인 이벤트와 
###           화면 동작과 관련 된 로직을 추가할 수 있다.
### created : 뷰 인스턴스가 생성되자마자 실행할 로직을 정의할 수 있는 속성. 뷰 인스턴스 라이프 사이클에 나온다.


### 뷰 인스턴스 유효 범위
Vue 생성자로 인스턴스를 생성하고 나서 화면에 인스턴스 옵션 속성을 적용하는 과정은 다음과 같다.

1. 뷰 라이브러리 파일 로딩
         ▼
2. 인스턴스 객체 생성(옵션 속성 포함)
         ▼
3. 특정 화면 요소에 인스턴스를 붙임
         ▼
4. 인스턴스 내용이 화면 요소로 변환
         ▼
5. 변환 된 화면 요소를 사용자가 최종 확인

~~~html
<div id="app">
  {{message}}
</div>
~~~

~~~vue
new Vue({
  el: '#app',
  data: {
    message: 'Hello Vue.js!'
  }

});
~~~

el 속성에 지정한 화면 요소에 인스턴스를 부착하는 과정
el 속성에 app ID를 지정하고 data 속성으로 출력할 파일을 작성한다.

~~~html
<div id="app">
  Hello Vue.js!
</div>
~~~

유효 범위(el 속성으로 지정해둠)을 벗어나면 인식이 안 되니 주의!
        
### 뷰 인스턴스 라이프 사이클
인스턴스의 속성 중 created. . . 
인스턴스가 생성되었을 때 호출할 동작을 정의하는 속성이다.
이처럼 인스턴스의 상태에 따라 호출할 수 있는 속성을 라이프 사이클(life cycle)속성이라고 한다.

그리고 각 라이프 사이클 속성에서 실행되는 커스텀 로직을 라이프 사이클 훅(hook)이라고 한다.

### 라이프 사이클 :  모바일 앱을 비롯하여 일반적으로 애플리케이션이 가지는 생명 주기
### 커스텀 로직 : 개발자가 임의로 작성한 추가 로직

![image](https://user-images.githubusercontent.com/57930450/69202991-8c901f00-0b86-11ea-94b7-596a1f88339a.png)

#### beforeCreate
인스턴스가 생성되고 나서 가장 처음으로 실행되는 라이프 사이클 단계.
이 단계에서는 data 속성과 methods 속성이 아직 인스턴스에 정의되어 있지 않고, 돔과 같은 화면 요소에도 접근할 수 없음.

#### created
beforeCreate 라이프 사이클 단계 다음에 실행되는 단계이다.
data 속성과 methods 속성이 정의되어 있기 때문에 this.data 또는 this.fetchData()와 같은 로직들을 이용하여 data 속성과 
methods 속성에 정의 된 값에 접근하여 로직을 실행할 수 있다.

다만, 아직 인스턴스가 화면 요소에 부착되기 전이기 때문에 template 속성에 정의 된 돔 요소로 접근할 수가 없다.

그리고 data 속성과 methods 속성에 접근할 수 있는 가장 첫 라이프 사이클 단계이자 컴포넌트가 생성되고 나서 실행되는 단계이기 때문에
서버에 데이터를 요청하여 받아오는 로직을 수행하기 좋다.

#### beforeMount
created 단계 이후 template 속성에 지정한 마크업 속성을 render()함수로 변환한 후 el 속성에 지정한 화면 요소(돔)에 인스턴스를 부착하기 전에
호출되는 단계이다.
#### render()는 자바스크립트로 화면의 돔을 그리는 함수이다.
render() 함수가 호출되기 직전의 로직을 추가하기 좋다.

#### mounted
el 속성에서 지정한 화면 요소에 인스턴스가 부착되고 나면 호출되는 단계로, template 속성에 정의한 화면 요소(돔)에 접근할 수 있어 화면 요소를
제어하는 로직을 수행하기 좋은 단계이다. 다만, 돔에 인스턴스가 부착되자마자 바로 호출되기 때문에 하위 컴포넌트나 외부 라이브러리에
의해 추가 된 화면 요소들이 최종 HTML 코드로 변환되는 시점과 다를 수 있다.

- 변환되는 시점이 다를 경우 $nextTick() API를 활용하여 HTML 코드로 최종 파싱(변환)될 때까지 기다린 후 돔 제어 로직을 추가한다.

#### beforeUpdate
el 속성에서 지정한 화면 요소에 인스턴스가 부착되고 나면 인스턴스에 정의한 속성들이 화면에 치환된다.
치환 된 값은 뷰의 반응성(Reactivity)을 제공하기 위해 $watch속성으로 감시한다.
이를 데이터 관찰이라고 한다.

- 뷰의 반응성: 뷰의 특징 중 하나로, 코드의 변화에 따라 화면ㅇ ㅔ반사적으로 반응하여 빠르게 화면을 갱신하는 것

또한 beforeUpdate는 관찰하고 있는 데이터가 변경되면 가상 돔으로 화면을 다시 그리기 전에 호출되는 단계이며, 변경 예정인 새 데이터에
접근할 수 있어 변경 예정 데이터의 값과 관련 된 로직을 미리 넣을 수 있다. 만약 여기에 값을 변경하는 로직을 넣더라도 화면이 다시 
그려지지는 않습니다.

#### updated
데이터가 변경되고 나서 가상 돔으로 다시 화면을 그리고 나면 실행되는 단계이다.
데이터 변경으로 인한 화면 요소 변경까지 완료 된 시점이므로, 데이터 변경 후 화면 요소 제어와 관련 된 로직을 추가하기 좋은 단계이다.
이 단계에서 데이터 값을 변경하면 무한 루프에 빠질 수 있기 때문에 값을 변경하려면 computed, watch와 같은 속성을 사용해야 한다.

따라서 데이터 값을 갱싱하는 로직은 가급적이면 beforeUpdate에 추가하고, updated에서 변경 데이터의 화면 요소(돔)와 관련 된 로직을 추가하는 것이 좋다.

- mounted 단계와 마찬가지로 하위 컴포넌트의 화면 요소와 외부 라이브러리에 의해 주입 된 요소의 최종 변환 시점이 다를 수 있다.
$nextTick()을 사용하면 변환이 완료될 때까지 기다렸다가 로직을 추가한다.

#### beforeDestroy
뷰 인스턴스가 파괴되기 직전에 호출되는 단계이다. 이 단계에서는 아직 인스턴스가 접근할 수 있다.
따라서 뷰 인스턴스의 데이터를 삭제하기 좋은 단계이다.

#### destroyed
뷰 인스턴스가 파괴되고 나서 호출되는 단계이다.
뷰 인스턴스에 정의한 모든 속성이 제거되고 하위에 선언한 인스턴들 또한 모두 파괴된다.

### 라이프 사이클 실습 예제
![image](https://user-images.githubusercontent.com/57930450/69204106-5a33f100-0b89-11ea-8d30-ece3035884e3.png)

브라우저에서 코드를 실행하고 개발자 도구 콘솔탭을 확인해보자!

![image](https://user-images.githubusercontent.com/57930450/69204186-8485ae80-0b89-11ea-8775-90d6cf7ac98c.png)

로그를 보면 뷰 라이프 사이클 도해의 흐름대로 모두 표시되는 것을 확인 할 수 있다.
의아한 점은 updated 속성 함수는 호출되지 않았다는 것! 왜 일까?

그 이유는 updated 라이프 사이클 훅은 뷰 인스턴스에서 데이터 변경이 일어난 화면이 다시 그려졌을 때 호출되는 로직이기 때문이다.
그럼 updated의 앞 단계인 mounted 단계에서 기존에 정의 된 data 속성의 message 값을 변경해보자

![image](https://user-images.githubusercontent.com/57930450/69204301-e34b2800-0b89-11ea-9b1b-ce116abb6791.png)

mounted 단계에서 데이터를 변경했기 때문에 beforeUpdate, updated 단계에 정의한 로직이 모두 동작한다.
다만, 여기서는 updated 단계에만 'updated'라는 로그를 출력하는 커스텀 로직을 정의했기 때문에 beforeUpdate 단계에서는 아무런
동작을 하지 않는다.

일단 message 값이 변경됨에 따라 화면의 내용도 자연스럽게 이해하고 넘어가자.

![image](https://user-images.githubusercontent.com/57930450/69204438-4046de00-0b8a-11ea-9922-e9ffb3e2861a.png)

아까는 보이지 않던 updated 로그가 출력되었다. 그 이유는 message의 값이 변경됨에 따라 화면에 표시되는 message 값이 갱신되었고, 이에 따라updated 속성에 정의한 로직이 실행되었기 때문이다. 여기서 중요한 것은 인스턴스의 데이터가 갱신되면서 라이프 사이클 단계가 beforeUpdate, updated 단계로 진입했다는 점이다. 이처럼 각 인스턴스 라이프 사이클레 맞춰 원하는 로직을 추가하여 원하는 시점에 실행할 수 있다.

뷰를 제대로 사용하려면 지금까지 배운 뷰 인스턴스 라이프 사이클을 잘 익혀야 한다!!!!

###  컴포넌트란?
컴포넌트(Component)란 조합하여 화면을 구성할 수 있는 블록(화면의 특정 영역)을 의미한다.

컴포넌트를 활용하면 화면을 빠르게 구조화하여 일괄적인 패턴으로 개발할 수 있다.

이렇게 화면의 영역을 컴포넌트로 쪼개서 재활용할 수 있는 형태로 관리하면 나중에 코드를 다시 사용하기가 훨씬 편하다.

또한 모든 사람들이 정해진 방식대로 컴포넌트를 등록하거나 사용하게 되므로 남이 작성한 코드를 직관적으로 이해 가능하다!!

ex)우리가 개발할 때 사용하던 네비게이션바, 사이드바, 헤더, 푸터, 콘텐츠 등이 분할 된 컴포넌트이다.

참고로 컴포넌트 간의 관계는 자료 구조의 트리 모양과 유사하다.

### 트리란? = 컴퓨터 자료 구조 중 하나로, 노드끼리의 연결이 부모 -자식의 구조를 따른다. 전체적인 모양이 나무와 비슷해서 트리라고 부른다. 트리는 윈도우 파일 시스템 체계를 비롯하여 각종 데이터베이스에서 활용되고 있고 뷰에서도 컴포넌트를 이해할 때 필요한 개념이다!

### 컴포넌트 등록하기
전역 컴포넌트 등록

전역 컴포넌트는 뷰 라이브러리를 로딩하고 나면 접근 가능한 Vue 변수를 이용하여 등록한다.

전역 컴포넌트를 모든 인스턴스에 등록하려면 Vue 생성자에서 .component()를 호출하여 수행하면 된다.

~~~Vue
Vue.component('컴포넌트 이름', {
  
  // 컴포넌트 내용

});
~~~

전역 컴포넌트 등록 형식에는 컴포넌트 이름과 컴포넌트 내용이 있다.

컴포넌트 이름은 template 속성에서 사용할 HTML 사용자 정의 태그 이름을 의미한다.

태그 이름의 명명 규칙은 HTML 사용자 정의 태그 스펙에서 강제하는 '모두 소문자'와 '케밥 기법'을 따르지 않아 된다!

### 사용자 정의 태그 : HTML 표준 태그들 이외에도 웹 개발자가 직접 정의하여 사용할 수 있는 태그
### 케밥 기법 : 변수가 단어의 조합으로 이루어져 있을 때, 단어와 단어 사이를 -로 잇는 변수 명명 방식

~~~Vue
       Vue.component('my-component', {
        template : '<div>전역 컴포넌트가 등록되었습니다.</div>'

       });

        new Vue({
          el: '#app'
        });
~~~
 
 지역 컴포넌트 만들기!
~~~Vue
      var cmp = {
        // 컴포넌트 내용
        template: '<div>지역 컴포넌트가 등록되었다.</div>'

      };

      new Vue({
          el: '#app',
          components: {
            'my-local-component' : cmp
          }
      });
~~~

따로 변수 선언을 해서 template 속성에 컴포넌트에서 수행할 내용을 작성하고
Vue 인스턴스에 components 속성에 컴포넌트 이름과 수행할 내용이 적힌 변수명을 적어준다!

아까 풀어본 전역 컴포넌트, 지역 컴포넌트 만들기

~~~JavaScript
Vue.component('todo-footer', {
  template: '<p>This is another global child component</p>'

});

var cmp = {

  template: '<p>This is another local child component</p>'

}

var app = new Vue({
  el: '#app',

  data: {
    message: 'This is a parent component'
  },

  components: {
      todo-list: cmp
  }
});

~~~

아직까진 훨씬 활용하기 쉬운 느낌!

### 뷰 컴포넌트 통신
컴포넌트 간 통신과 유효 범위

앵귤러1이나 백본(Backbone.js)과 같은 초창기 자바스크립트 프레임워크에서는 한 화면을 1개의 View로 간주했다!

따라서 한 화면의 데이터를 해당 화면 영역 어디서든지 호출할 수 있었다.

하지만 Vue.js의 경우 컴포넌트로 화면을 구성하므로 같은 웹페이지라도 데이터를 공유할 수가 없다. 

그 이유는 컴포넌트마다 자체적으로 고유한 유효 범위(scope)를 갖기 때문이다.

이는 뷰 프레임워크 내부적으로 정의 된 특징이다.

따라서 각 컴포넌트의 유효 범위가 독립적이기 때문에 다른 컴포넌트의 값을 직접적으로 참조할 수가 없다!!

~~~Vue
    <script>
      var cmp1 = {

        template: '<div>첫 번째 지역 컴포넌트 : {{ cmp1Data }}</div>',

        data: function () {
          return {
            cmp1Data : 100
          }
        }
      };

      // 두번째 컴포넌트 내용

      var cmp2 = {

        template: '<div>두 번째 지역 컴포넌트 : {{ cmp2Data }}</div',
        data: function () {
          return {
            cmp2Data : cmp1.data.cmp1Data
          }
        }
      }

      new Vue({
        el: '#app',
        components: {
          'my-component1': cmp1,
          'my-component2': cmp2
        }
      });
    </script>
~~~
위 예제를 코딩해보면 책에서 나온데로 화면에서는 1번 컴포넌트 값 100은 나오지만 2번은 나오지 않는다

다른 컴포넌트의 값을 직접 참조할 수가 없기 때문이라고 한다.

컴포넌트의 유효 범위로 이냏 다른 컴포넌트의 값을 직접 접근하지 못 하기 때문에 나타나는 결과이다!!

이렇게 다른 컴포넌트의 값을 참조하지 못 하기 때문에 생기는 특징도 있다.

뷰에서 미리 정의해 놓은 데이터 전달 방식에 따라 일관 된 자료 구조로 어플리케이션을 작성하게 된다.

그러므로 개발자 개개인의 스타일대로 구성되지 않고, 어플리케이션의 모두 동일한 데이터 흐름을 갖는다.

이렇게 되면 다른 사람의 코드를 빠르게 파악할 수 있어 협업하기에도 좋다.

### 상, 하위 컴포넌트 관계
각 컴포넌트는 유효 범위를 갖고 있기 때문에 직접 다른 컴포넌트의 값을 참조할 수 없다!

따라서 뷰 프레임워크 자체에서 정의한 컴포넌트 데이터 전달 방법을 따라야 한다.

가장 기본적인 데이터 전달 방법은 바로 상위(부모) - 하위(자식) 컴포넌트 간의 데이터 전달 방법이다.

트리 구조이다..! 

지역 또는 전역 컴포넌트를 등록하면 등록 된 컴포넌트는 자연스레 하위 컴포넌트(자식)가 된다.

그리고 하위 컴포넌트를 등록한 인스턴스는 상위 컴포넌트(부모)가 된다.

(상위 컴포넌트) => [props 전달] => (하위 컴포넌트) => [이벤트 발생] => (상위 컴포넌트) . . .

이렇게 순환 된다.

먼저 상위에서 하위로는 props라는 특별한 속성을 전달한다.

그리고 하위에서 상위로는 기본적으로 이벤트만 전달할 수 있다.

그러면 각 전달 방법에 대해 살펴보자!!

## 이벤트와 함께 데이터를 전달하고 싶은 경우에는 이벤트의 두 번째 인자 값으로 전달하거나 이벤트 버스(Event Bys) 활용 방법이 있다.

~~~HTML
    <div id="app">
      <child-component v-bind:propsdata="message"></child-component>
    </div>
~~~
~~~Vue
    <script>
      Vue.component('child-component', {
          props: ['propsdata'],
          template: '<p>{{ propsdata }}</p>',
      });

      new Vue({
        el: '#app',

        data: {
          message: 'Hello Vue! passed from Parent Component'
        }
      });

    </script>
~~~

작성해야 될 코드 순서대로 정리!!
1. new Vue()로 인스턴스를 하나 생성한다.

2. Vue.component()를 이용하여 하위 컴포넌트인 child-component를 등록한다.

3. child-component의 내용에 props 속성으로 propsdata를 정의한다.

4. HTML에 컴포넌트 태그를 추가한다. <child-component>태그의 v-bind 속성을 보면, v-bind:propsdata="message"는
  상위 컴포넌트의 message 속성 값인 Hello Vue! passed from Parent Component 텍스트를 하위 컴포넌트의 propsdata로 전달한다.
  
5. child-component의 template 속성에 정의 된 <p>{{ propsdata }}</p>는 Hello Vue! passed from Parent Component가 된다.

위 과정을 더 간단히 정리하면 뷰 인스턴스의 data 속성에 정의 된 message 속성을 하위 컴포넌트에 props로 전달하여 화면에 나타난다.

### 하위에서 상위 컴포넌트로 이벤트 전달하기

이벤트 발생과 수신

앞에서 배운 props는 상위에서 하위 컴포넌트로 데이터를 전달하는 방식이다. 그럼 반대로 하위 컴포넌트에서 상위 컴포넌트로의

통신은 어떻게 할까?

이벤트를 발생시켜(event emit) 상위 컴포넌트에 신호를 보내면 된다.

상위 컴포넌트에서 하위 컴포넌트의 특정 이벤트가 발생하기를 기다리고 있다가 하위 컴포넌트에서 특정 이벤트가 발생하면 상위 컴포넌트에서

해당 이벤트를 수신하여 상위 컴포넌트의 메서드를 호출하는 것이다.

### 하위에서 상위 컴포넌트로 데이터를 전달할 수는 없을까?
뷰 공식 사이트의 이벤트 발생 사용 방법에서는 하위에서 상위로 데이터를 전달하는 방법을 다루지 않는다.

왜냐하면 이는 뷰의 단방향 데이터 흐름에 어긋나는 구현 방법이기 때문이다.

하지만 향후에 복잡한 뷰 어플을 구출할 때 이벤트 버스(Event Bus)를 이용하여 데이터를 전달해야 할 경우가 있기 때문이다


### 이벤트 발생과 수신 형식
이벤트 발생과 수신은 $emit()과 v-on: 속성을 사용하여 구현한다. 각각의 형식은 아래와 같다.

~~~Vue
// 이벤트 발생
this.$emit('이벤트명');
//$emit()을 이용한 이벤트 발생

// 이벤트 수신
<child-component v-on:이벤트명="상위 컴포넌트의 메서드명"></child-component>
//v-on: 속성을 이용한 이벤트 수신
~~~

$emit()을 호출하면 괄호 안에 정의 된 이벤트가 발생한다. 그리고 일반적으로 $emit()을 호출하는 위치는 하위 컴포넌트의
특정 메서드 내부이다. 따라서 $emit()을 호출할 때 사용하는 this는 하위 컴포넌트를 가리킨다.

호출한 이벤트는 하위 컴포넌트를 등록하는 태그(상위 컴포넌트의 template 속성에 위치)에서 v-on:으로 받는다.

하위 컴포넌트에서 발생한 이벤트명을 v-on: 속성에 지정하고, 속성의 값에 이벤트가 발생했을 때 호출 될 상위 컴포넌트의 메서드를 지정한다.

~~~html
    <div id="app">
        <child-component v-on:show-log="printText"></child-component>
    </div>
~~~

~~~Vue
        Vue.component('child-component', {
          template: '<button v-on:click="showLog">show</button>',
          methods: {
            showLog: function() {
              this.$emit('show-log');
            }
          }
        });

        var app = new Vue({
          el: '#app',
          data: {
              message: 'Hello Vue! passed from Parent Component'
          },
          methods: {
            printText: function() {
              console.log("received an event");
            }
          }
        });
~~~

실습 코딩 공부

html div태그에 컴포넌트 태그를 넣고
v-on 속성을 사용해서 이벤트명을 정의해준다.

 <child-component v-on:show-log="printText"></child-component>
 
 v-on:show-log="printText" / show-log는 하위 컴포넌트의 이벤트명이고,
 
 printText는 상위 컴포넌트의 메서드명이다.
 
 아직은 솔직히 v-on속성의 용법을 잘 모르겠지만 넘어가자.
 
         Vue.component('child-component', {
          template: '<button v-on:click="showLog">show</button>', // 버튼 요소를 추가한다.
          methods: { // 메서드를 추가한다.
            showLog: function() {
              this.$emit('show-log'); // 이벤트 발생 로직.
            }
          }
        });
        
        var app = new Vue({
          el: '#app',
          data: {
              message: 'Hello Vue! passed from Parent Component'
          },
          methods: {
            printText: function() {
              console.log("received an event");
            }
          }
        });
        
 child-component의 [show]버튼을 클리가형 이벤트를 발생시키고, 발생한 이벤트로 상위 컴포넌트(이것만 놓고보면 루트 컴포넌트라고 한다.)의
 
 printText() 메서드를 빌행시키는 예제였다!!
 
 1. [show] 버튼을 브라우저에서 클릭하면 클릭 이벤트 v-on:click="showLog"에 따라서 showLog 메서드가 실행된다.
 2. showLog() 메서드 안에 this.$emit('show-log')가 실행되면서 show-log 이벤트가 발생한다.
 3. show-log 이벤트는 <child-component>에 정의한 v-on:show-log에 전달되고, v-on:show-log의 대상 메서드인 최상위 컴포넌트 메서드
    printText()가 실행된다.
 4. printText()는 received an event라는 로그를 출력하는 메서드이므로 마지막으로 콘솔에 로그가 출력된다.
  
  ### 같은 레벨의 컴포넌트 간 통신
상위에서 하위로 props를 전달하고, 하위에서 상위로 이벤트를 전달했다.

이번에는 상위-하위 관계가 아니라 같은 레벨에 있는 컴포넌트끼리 어떻게 통신하는지 알아보자.

![image](https://user-images.githubusercontent.com/57930450/69780808-a3222000-11ef-11ea-9f55-04d0bb0db92f.png)

앞 그림은 같은 상위 컴포넌트를 가지는 2개의 하위 컴포넌트를 나타낸다.

뷰는 상위에서 하위로만 데이터를 전달해야 하는 기본적인 통신 규칙을 따르기 때문에 바로 옆 컴포넌트에 값을 전달하려면

하위에서 공통 상위 컴포넌트로 이벤트를 전달한 후 공통 상위 컴포넌트에서 2개의 하위 컴포넌트에 pops를 내려 보내야 한다.

이런 방식으로 통신해야 하는 이유는 컴포넌트 고유의 유효 범위 때문이다.

다른 컴포넌트의 값을 직접 참조하지 못하므로 기본적인 데이터 전달 방식을 활용하여 같은 레벨 간에 통신이 가능하도록 구조를 갖춰야 한다.


하지만 이런 통신 구조를 유지하다 보면 상위 컴포넌트가 필요 없음에도 불구하고 같은 레벨 간에 통신하기 위해 강제로 상위 컴포넌트를 두어야 하는 경우가 발생한다.

이를 해결하는 방법이 바로 이벤트 버스이다.

### 관계 없는 컴포넌트 간 통신 - 이벤트 버스
이벤트 버스(Event Bus)는 개발자가 지정한 2개의 컴포넌트 간에 데이터를 주고받을 수 있는 방법이다.

앞에서 배운 컴포넌트 통신은 항상 상위 - 하위 구조를 유지해야만 데이터를 주고 받을 수 있다.

이벤트 버스를 이용하면 이런 상위 - 하위 관계를 유지하고 있지 않아도 데이터를 한 컴포넌트에서 다른 컴포넌트로 전달할 수 있다.

![image](https://user-images.githubusercontent.com/57930450/69781117-863a1c80-11f0-11ea-944a-b3233642985f.png)

취하위에 있는 하위 컴포넌트 B에서 상위 컴포넌트 A로 데이터를 전달하려면?

뷰에서 제시하는 기본적인 컴포넌트 통신 방식을 생각했을 때 하위 컴포넌트 B, 상위 컴포넌트 B, 최상위 컴포넌트를 거쳐서 상위 컴포넌트 A까지
가야 한다. 하지만 웹 앱이 커져 컴포넌트가 많아지면 이런 식의 데이터 전달 방식은 매우 번거롭다!!!

이럴 경우 이벤트 버스를 활용하면 중간 컴포넌트들을 거치지 안혹 하위 컴포넌트 B에서 상위 컴포넌트 A로 바로 데이터를 전달할 수 있어 편하다.

이벤트 버스 형식 연습
~~~Vue
// 이벤트 버스를 위한 추가 인스턴스 1개 생성
var eventBus = new Vue();

// 이벤트를 보내는 컴포넌트
methods: {
  메서드명: function() {
      eventBus.$emit('이벤트명', 데이터);
  }
}

// 이벤트를 받는 컴포넌트
methods: {
  created: function() {
    eventBus.$on('이벤트명', function(데이터) {
      ...
    });
  }
}
~~~

어플 로직을 담는 인스턴스와 별개로 새로운 인스턴스를 1개 더 생성하고, 새 인스턴스를 이용하여 이벤트를 보내고 받는다.

보내는 컴포넌트에서는 $emit()을, 받는 컴포넌트에서는 $on을 구현한다.

실습
~~~html
<html>
  <head>
      <title>Document</title>
  </head>
<body>
    <div id="app">
        <child-component></child-component>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/vue@2.5.2/dist/vue.js"></script>
    <script>

        var eventBus = new Vue();

        Vue.component('child-component', {
          template: '<div>하위 컴포넌트 영역입니다.<button v-on:click="showLog">show</button></div>',
          methods:{
            showLog: function() {
              eventBus.$emit('triggerEventBus', 100);
            }
          }
        });

        var app = new Vue({
          el: '#app',
          created: function() {
              eventBus.$on('triggerEventBus', function(value) {
                  console.log("이벤트를 전달받음. 전달받은 값 : ", value);
              });
          }
        });



    </script>
</body>
</html>
~~~

약간 아리까리한게 있어서 코드에서 모르는 부분을 정리하고 넘어간다...!

## DOM 옵션들
### el 속성
타입 : string, element
제한 사항 : Vue 인스턴스에서만 사용 가능

Vue 인스턴스를 생성했을 때 html 요소(DOM)를 마운트하는데 사용한다..!

### props 속성
타입 : Array<string> | Object
++부모 컴포넌트의 데이터를 받을 수 있게 노출++ 된 속성의 리스트/해시이다.
  
 단순한 배열 기반 구문과 사용자 지정 유효성 검사 및 기본값과 같은 고급 구성을 허용하는 Object 기반 구문이 있다.
 
 

### template 속성
타입 : string

Vue 인스턴스의 마크업으로  사용할 문자열 템플릿이다. 
템플릿은 마운트 된 엘리먼트를 대체한다.

### methods
타입 : { [key:string]: Function }

Vue 인스턴스에 추가할 메소드이다. VM 인스턴스를 통해 직접 접근하거나 디렉티브 표현식에서 사용할 수 있다.
모든 메소드는 자동으로 this 컨텍스트를 Vue 인스턴스에 바인딩한다.(핵심)

this 컨텍스트를 내포하고 있기 때문에 key로 지정되는 문자열을 스코프 안에 this.key를 하면 정의 되지 않는다고 한다.

## 옵션  / 라이프사이클 훅
모든 라이프 사이클 훅은 자동으로 ++this 컨텍스트를 인스턴스에 바인딩++하므로 데이터, 계산 된 속성 및 메소드에 접근할 수 있다.

즉, 화살표 함수를 사용해 라이프 사이클 메소드를 정의하면 안 된다.

### created 
타입 : Function

++인스턴스가 작성 된 후 동기적으로 호출된다.++ 이 단계에서 인스턴스는 데이터 처리, 계산 된 속성, 메소드, 감시/이벤트 콜백 등과같은 옵션 처리를 완료한다. 그러나 마운트가 시작되지 않았으므로 $el 속성을 아직 사용할 수 없다.

## 인스턴스 메소드 / 이벤트
### vm.$emit(eventName,[...args])

전달인자 : {String} event , [...args]

현재 인스턴스에서 이벤트 트리거를 추가한다. 추가 인자는 리스너의 콜백 함수로 전달된다.

### vm.$on(event, callback)
전달인자 : {string | Array<string>} event (객체는 2.2.0버전 이상에서만 지원)
           {Function} callback
  
현재 VM에서 사용자 정의 이벤트를 듣는다.
이벤트는 vm.$emit에 의해 호출 될 수 있다. 콜백은 이러한 이벤트 트리거 메소드에 전달 된 모든 추가 인수를 수신한다.


## 디렉티브
### v-on
전달인자 : event
엘리먼트에 이벤트 리스너를 연결한다. 이벤트 유형은 전달인자로 표시된다.
표현식은 메소드 이름 또는 인라인 구문일 수 있으며, 수식어가 있으면 생략할 수 있다.

일반 엘리먼트에 사용되면 기본 DOM 이벤트만 받는다.
사용자 정의 컴포넌트에서 사용될 때 해당 하위 컴포넌트에 생성 된 사용자 정의 이벤트를 받는다.

네이티브 DOM 이벤트를 수신하면 메소드는 네이티브 이벤트를 유일한 전달인자로 받는다.

인라인 구문을 사용하는 경우 명령문은 특별한 $event 속성에 접근할 수 있다.

~~~html
<html>
  <head>
      <title>Document</title>
  </head>
<body>
    <div id="app">
       <child-component></child-component>  
    </div>

    <script src="https://cdn.jsdelivr.net/npm/vue@2.5.2/dist/vue.js"></script>
    <script>

      var eventBus = new Vue();

      Vue.component('child-component', {

        // Vue Dom 옵션들 중 하나, 마크업으로 사용되고, 마운트 된 엘리먼트를 대체한다.
        template: '<div>하위 컴포넌트 영역<button v-on:click="showLog">Show</button></div>',

        // Vue Dom 옵션들 중 하나, 이벤트 함수를 작성하고 메소드를 구체적으로 작성하는 것 
        methods:{
          // 이벤트 이름 적고
          showLog:function () {
            // vm / 인스턴스 메소드 $emit으로 이벤트 트리거를 적는다, 추가 인자는 리스너의 콜백 함수이다.
            eventBus.$emit('triggerEventBus', 100);
          }
        }
      });

      var app = new Vue({
        // DOM 옵션 중 el 속성. . . DOM을 마운트한다.
        el: '#app',
        // 라이프 사이클 훅 인스턴스가 작성 된 후 동기적으로 작동된다.
        created: function () {
          // 인스턴스 메소드 $on으로 트리거를 받는다.
          eventBus.$on('triggerEventBus', function(value) {
            console.log("이벤트를 전달받음", value);
          });
        }        
      });

    </script>
</body>
</html>
~~~

컴포넌트에서 DOM으로 prop 속성 활용해서 데이터 출력하기
~~~html
<html>
  <head>
      <title>Document</title>
  </head>
<body>
    <div id="app">
        <child-component v-bind:propsdata="message"></child-component>
        <sibling-component v-bind:propsdata2="anotherMessage"></sibling-component>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/vue@2.5.2/dist/vue.js"></script>
    <script>

      Vue.component('child-component', {
        props: ['propsdata'],
        template: '<p>{{ propsdata }}</p>'
      });

      Vue.component('sibling-component', {
        props:['propsdata2'],
        template: '<p>{{ propsdata2 }}</p>'

      });

      var app = new Vue({
        el: '#app',

        data: {
          message: 'Hello Vue! passed from Parent component',

          anotherMessage: '어나더 메시지'
        }
      });



    </script>
</body>
</html>
~~~
