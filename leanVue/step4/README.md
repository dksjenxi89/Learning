[Do it! vue.js - 장기효] {http://www.yes24.com/Product/Goods/58206961?Acode=101}

## 상용 웹 앱을 개발하기 위한 필수 기술들
- 라우터 & HTTP 통신

###  뷰 라우터

라우팅이란?
라우터를 이해하기 위해서는 먼저 라우팅(Routing)이 무엇인지 알아야 한다.

라우팅이란 웹 페이지 간의 이동 방법을 말한다.

라우팅은 현대 웹 앱 형태 중 하나인 싱글 페이지 어플리케이션(SPA)에서 주로 사용되고 있다.

### 싱글 페이지 어플리케이션이란?
페이지를 이동할 때마다 서버에 웹 페이지를 요청하여 새로 갱신하는 것이 아니라 미리 해당 페이지들을 받아 놓고
페이지 이동 시에 클라이언트의 라우팅을 이용하여 화면을 갱신하는 패턴을 적용한 어플리케이션

라우팅을 이용하면 화면 간의 전환이 매끄러울 뿐만 아니라 어플리케이션의 사용자 경험을 향상시킬 수 있다.

일반적으로 브라우저에서 웹 페이지를 요청하면 서버에서 응답을 받아 웹 페이지를 다시 사용자에게 돌려주는 시간 동안 화면 상에 깜빡거림 현상이 나타난다.
이런 부분들을 라우팅으로 처리하면 깜빡거림 없이 화면을 매끄럽게 전환할 수 있을 뿐만 아니라 더 빠르게 화면을 조작할 수 있어 사용자 경험이 향상된다.

뷰뿐만 아니라 리액트와 앵귤러 모두 라우팅을 이용하여 화면을 전환하고 있으며, 프런트 엔드 프레임워크를 사용하지 않고 일반 HTML 파일들로도 라우팅 자바스크립트 라이브러리를
이용하여 라우팅 방식의 페이지 이동을 구현할 수 있다.


### 뷰 라우터
뷰 라우터는 뷰에서 라우팅 기능을 구현할 수 있도록 지원하는 공식 라이브러리이다.
뷰 라우터를 이용하여 뷰로 만든 페이지 간에 자유롭게 이동할 수 있다.

뷰 라우터를 구현할 때 필요한 특수 태그와 기능은 다음과 같다.

### 뷰 라우터 태그 정리

~~~html
<router link to="URL 값"> // 페이지 이동 태그. 화면에서는 <a>로 표시되며 클릭하면 to에 지정한 URL로 이동한다.

<router-view> // 페이지 표시 태그. 변경되는 URL에 따라 해당 컴포넌트를 뿌려주는 영역이다.
~~~

~~~html
<html>
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vue Router Sample</title>
  </head>
  <body>
    <div id="app">
      <h1>뷰 라우터 예제</h1>
      <p>
        <router-link to="/main">Main 컴포넌트로 이동</router-link>
        <router-link to="/login">Login 컴포넌트로 이동</router-link>
      </p>
      <router-view></router-view>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/vue@2.5.2/dist/vue.js"></script>
    <script src="https://unpkg.com/vue-router@3.0.1/dist/vue-router.js"></script> // vue router cdn 추가

    <script>
      var Main = { template: '<div>main</div>' };
      var Login = { template: '<div>login</div>'};

      var routes = [
        { path: '/main', component: Main },
        { path: '/login', component: Login }
      ];

      var router = new VueRouter({
        routes
      });

      var app = new Vue({
        router
      }).$mount('#app');
    </script>
  </body>
</html>
~~~

### 인스턴스 메소드 / 라이프사이클

vm.$mount([elementOrSelector]) 

전달인자 :
{Element | string} [elementOrSelector]
{boolean} [htdrating]

반환 값 : vm - 인스턴스 그 자체

Vue 인스턴스가 인스턴스화 할 때 el 옵션이 없으면 연결 된 DOM 앨리먼트 없이
"unmounted" 상태가 된다.

vm.$mount는 unmounted 된 Vue 인스턴스의 마운트를 수동으로 시작하는데 사용할 수 있다.

elementOrSelector 인자가 제공되지 안흥면, 템플릿은 문서가 아닌 엘리먼트로 렌더링 될 것이므로 DOM API를 사용하여
문서에 직접 삽입해야 한다.

이 메소드는 다른 인스턴스 메소드를 체이닝할 수 있도록 인스턴스 그 자체를 반환한다.

### Vue Router 정리
### <router-link>는 라우터 지원 앱에서 사용자 네비게이션을 가능하게 하는 컴포넌트이다.
목표 위치는 to prop로 지정된다. 

<router link> 태그는 다음과 같은 이유로 하드 코딩 된 <a href="...">보다 선호된다.

- HTML5 히스토리 모드와 해시 모드에서 모두 동일한 방식으로 작동하므로 모드를 트랜지션하기로 결정하거나
라우터가 IE9에서 해시 모드로 트랜지션 한 경우 변경할 필요가 없다.

- HTML5 히스토리 모드에서, router-link는 클릭 이벤트를 차단하여 브라우저가 페이지를 다시 로드하지 않도록 한다. 

- HTML5 히스토리 모드에서 base 옵션을 사용할 때 to prop의 url에 이를 포함할 필요가 없다.

#### to 속성
링크의 대상 라우트를 나타낸다. to prop의 값은 내부적으로 router.push()에 전달 될 것이므로 값은 문자열이나 위치 디스크랩터 객체가 될 수 있다.



### <router-view> 컴포넌트는 주어진 라우트에 대해 일치하는 컴포넌트를 렌더링하는 함수형 컴포넌트이다.
<router-view>에서 렌더링 된 컴포넌트는 자체 <router-view>를 포함 할 수 있으며, 이는 중첩 된 라우트를 위해
컴포넌트를 렌더링한다.

### 네스티드 라우터 : 여러 개의 컴포넌트를 동시에 표시할 수 있는 라우터인 네스티드 라우터

라우터로 페이지를 이동할 때 최소 2개 이상의 컴포넌트를 화면에 나타낼 수 있다.

네스티드라는 단어에서 추측할 수 있듯이 상위 컴포넌트 1개에 하위 컴포넌트 1개를 포함하는 구조로 구성 된다.

<html>
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vue Nested Router</title>
  </head>
  <body>
    <div id="app">
        <router-view></router-view> <!-- 상위 컴포넌트가 뿌려질 영역 -->
    </div>

    <script src="https://cdn.jsdelivr.net/npm/vue@2.5.2/dist/vue.js"></script>
    <script src="https://unpkg.com/vue-router@3.0.1/dist/vue-router.js"></script>

    <script>
        // 각 객체를 정의한다. 
        var User = {
          template:'<div>User Component<router-view></router-view></div>' // 라우터뷰가 하나 더 있다는게 포인트
        };
        var UserProfile = { template: '<p>User Profile</p>' };
        var UserPost = { template: '<p>User Post</p>' };

        var routes = [
          {
          path: '/user',
          component: User,
          children: [{path: 'posts', component: UserPost}, {path: 'profile', component: UserProfile}]
        }
        ];

        var router = new VueRouter({
          routes
        });

        var app = new Vue({
          router
        }).$mount('#app');

    </script>
  </body>
</html>

네스티드 라우터는 화면을 구성하는 컴포넌트의 수가 적을 때는 유용하지만 한 번에 더 많은 컴포넌트를 표시하는 데는 한계가 있다.

이 문제를 해결할 수 있는 방안으로 네임드 뷰가 있다.

### 네임드 뷰
특정 페이지로 이동했을 때의 컴포넌트를 동시에 표시하는 라우팅 방식이다.
앞에서 다룬 네스티드 라우터는 상위 컴포넌트가 하위 컴포넌트를 내포하는 방식이지만

네임드 뷰는 같은 레벨에서 여러 개의 컴포넌트를 한 번에 표시한다.

~~~html
<html>
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vue Named View</title>
  </head>
  <body>
    <div id="app">
      <router-view name="appHeader"></router-view>
      <router-view></router-view> <!-- name 을 지정하지 않았을 경우에는 디폴트이다.-->
      <router-view name="appFooter"></router-view>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/vue@2.5.2/dist/vue.js"></script>
    <script src="https://unpkg.com/vue-router@3.0.1/dist/vue-router.js"></script>

    <script>
        var Body = { template: '<div>This is Body</div>' };
        var Header = { template: '<div>This is Head</div>' };
        var Footer = { template: '<div>This is Footer</div>' };

        var router = new VueRouter({
          routes: [
            {
              path: '/',
              components: {
                default: Body,
                appHeader: Header,
                appFooter: Footer
              }
            }
          ]
        });

        var app = new Vue({
          router
        }).$mount('#app');
    </script>
  </body>
</html>
~~~

~~~
<html>
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vue Named View</title>
  </head>
  <body>
    <div id="app">
      <router-view name="header"></router-view>
      <router-view></router-view>
      <router-view name="footer"></router-view>
      <router-view name="loginHeader"></router-view>
      <router-view name="loginFooter"></router-view>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/vue@2.5.2/dist/vue.js"></script>
    <script src="https://unpkg.com/vue-router@3.0.1/dist/vue-router.js"></script>

    <script>
        var Body = { template: '<div>This Body</div>' };
        var Header = { template: '<div>This Header</div>' };
        var Footer = { template: '<div>This Footer</div>' };
        var LoginBody = { template: '<div>This LoginBody</div>' };
        var LoginHeader = { template: '<div>This LoginHeader</div>' };
        var LoginFooter = { template: '<div>This LoginFooter</div>' };

      var router = new VueRouter({
        routes: [
            {
              path: '/',
              components: {
                default: Body,
                header: Header,
                footer: Footer
              }
            },
            {
                path: '/login',
                components: {
                    default: LoginBody,
                    loginHeader: LoginHeader,
                    loginFooter: LoginFooter
                }
            }
        ]
      });

      var app = new Vue({
        router
      }).$mount('#app');
    </script>
  </body>
</html>
~~~

네임드 뷰를 활용한 실습

### 뷰 HTTP 통신

웹 앱의 HTTP 통신 방법
요즈음 웹 앱에서 서버에 데이터를 요청하는 HTTP 통신은 필수로 구현해야 하는 기능이다. 
과거의 웹 사이트가 정적인 텍스트나 간단한 이미지를 나타내는 데 그쳤다면 이제는 사용자와의 상호 작용에 따라 데이터를 동적으로 화면에 표시해 줘야 
하기 때문이다.

### 프로토콜: 컴퓨터나 단말기 간에 통신하기 위해 상호간에 정의한 규칙

여기서 HTTP는 브라우저와 서버 간에 데이터를 주고 받는 통신 프로토콜이다.

브라우저에서 데이터를 보내달라고 요청을 보내면 서버에서 응답으로 해당 데이터를 보내주는 방식이다.

서버에 '해당 데이터를 보내주세요.'라는 메시지를 보내는게 바로 'HTTP 요청을 보낸다'와 같은 의미이다.

웹 앱 HTTP 통신의 대표적인 사례로는 제이쿼리(jQuery)의 ajax가 있습니다.
ajax는 서버에서 받아온 데이터를 표시할 때 화면 전체를 갱신하지 않고도 화면의 일부분만 변경할 수 있게 하는 자바스크립트 기법이다.

ajax가 대중화되면서 많은 웹 앱에서 ajax를 사용하고 있다.

리액트, 앵귤러 등에서도 활발하게 사용되고 있다.

뷰에서도 마찬가지로 ajax를 지원하기 위한 라이브러리를 제공한다. 뷰 프레임워크의 필수 라이브러리로 관리하던 뷰 리소스와
요즘 가장 많이 사용하는 액시오스(axios)가 바로 그것이다.

### 뷰 리소스
뷰 리소스(resource)는 초기에 코어 팀에서 공식적으로 권하는 라이브러리였으나 2016년 말에 에반이 공식적인 지원을 중단하기로 결정하면서
다시 기존에 관리했던 PageKit 팀의 라이브러리로 돌아갔다.

그 이유는 HTTP 통신 관련 라이브러리는 뷰 라우팅, 상태 관리와 같은 라이브러리와는 다르게 프레임워크에 필수적인 기능이 아니라고 판단했기 때문이다.

그럼에도 불구하고 뷰 리소스는 아직 계속 사용할 수 있는 라이브러리이기 때문에 간단히 살펴본다!!

뷰 리소스를 사용하는 방법은 CDN을 이용해서 라이브러리를 로딩하는 방식과 NPM으로 라이브러리를 설치하는 방법(ES6 기준)이 있다.

CDN 설치 방법을 이용하여 간단히 뷰 리소스로 서버에서 특정 데이터를 받아와 로그로 출력하는 실습을 해본다!

~~~html
<html>
<head>
  <title>Vue Resource Sample</title>
</head>
<body>
  <div id="app">
    <button v-on:click="getData">프레임워크 목록 가져오기</button>
  </div>

  <script src="https://cdn.jsdelivr.net/npm/vue@2.5.2/dist/vue.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/vue-resource@1.3.4"></script>
  <script>
    new Vue({
      el: '#app',
      methods: {
        getData: function() {
          this.$http.get(`https://raw.githubusercontent.com/joshua1988/doit-vuejs/master/data/demo.json`)
              .then(function(response) {
                console.log(response);
                console.log(JSON.parse(response.data));
              });
        }
      }
    });
  </script>
</body>
</html>
~~~

### 액시오스
액시오스는 현재 뷰 커뮤니티에서 가장 많이 사용되는 HTTP 통신 라이브러리이다.

에반도 뷰 리소스 라이브러리를 공식 라이브러리에서 제외하면서 액시오스를 언급했다고 한다.

액시오스는 깃허브 리포지토리의 별이 3만 개가 넘는데, 이는 뷰 리소스의 8천 개에 비해 압도적으로 많다.

그만큼 많은 개발자들이 관심을 갖고 이용하고 있다는 증거이다. 일반적으로 오픈 소스 라이브러리의 장래성은 깃 허브 리포지토리가

얼마나 활성화되어 있느냐로 판단할 수 있는데, 액시오스가 그런 면에서는 뷰 리소스보다 더 안정적으로 지원되는 라이브러리라고 할 수 있다.


또한 액시오스는 Promise 기반의 API 형식이 다양하게 제공되어 별도의 로직을 구현할 필요 없이 주어진 API만으로도 간편하게 원하는 로직을
구현할 수 있다.

### Promise 기반의 API 형식이란 무엇일까?
Promise란 서버에 데이터를 요청하여 받아오는 동작과 같은 비동기 로직 처리에 유용한 자바스크립트 객체이다.

자바스크립트는 단일 스레드로 코드를 처리하기 때문에 특정 로직의 처리가 끝날 때까지 기다려 주지 않는다.

따라서 데이터를 요청하고 받아올 때까지 기다렸다가 화면에 나타내는 로직을 실행해야 할 때 주로 Promise를 활용한다.

그리고 데이터를 받아왔을 때 Promise로 데이터를 화면에 표시하거나 연산을 수행하는 등 특정 로직을 수행한다.

데이터 통신과 관련한 여러 라이브러리 대부분에서 Promise를 활용하고 있으며, 액시오스에서도 Promise 기반의 API를 지원한다.

액시오스 사용 cdn
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>

액시오스로 요청 방식 예제

html에서
~~~html
  axios.get('URL 주소').then().catch();
  
  axios.post('URL 주소').then().catch();
~~~

스크립트에서
~~~script
  axios({
    method: 'get',
    url: 'URL 주소',
    . . .
  });
~~~

api 유형
- axios.get('URL 주소').then().catch()

처리 결과
해당 url 주소에 대해 http get 요청을 보낸다.

서버에서 보낸 데이터를 정상적으로 받아오면 **then() 안에 정의한 로직이 실행**되고,

데이터를 받아올 때 오류가 발생하면 **catch()에 정의한 로직이 수행**된다.

axios.post('url 주소').then().catch()

물론 위와 똑같고 post 방식으로 요청 방식만 변경 될 뿐이다.

catch문은 생략 가능하다!! 

- axios{{옵션 속성}}
http 요청에 대한 자세한 속성들을 직접 정의하여 보낼 수 있다.

데이터를 보낼 때 url, http 요청 방식, 보내는 데이터 유형, 기타 등등

~~~html
<html>
  <head>
      <title>Vue with Axios Sample</title>
  </head>
<body>
    <div id="app">
        <button v-on:click="getData">프레임워크 목록 가져오기</button>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/vue@2.5.2/dist/vue.js"></script>
    <script src="https://unpkg.com/axios/dist/axios.min.js"></script>

    <script>

      new Vue({
        el: '#app',
        methods: {
          getData: function() {
            axios.get('https://raw.githubusercontent.com/joshua1988/doit-vuejs/master/data/demo.json')
            .then(function(response) {
              console.log(response);
            });
          }
        }
      });

    </script>
</body>
</html>
~~~

![image](https://user-images.githubusercontent.com/57930450/70300636-5a93e380-183b-11ea-82ec-9026025cf86e.png)

개발자 모드에서 response 객체를 확인해보면 일반 문자열이 아니라 객체 속성이기 때문에

vue resource와는 다르게 JSON.parse()를 사용하여 객체로 변환할 필요가 없다.

이런 부분 때문에 뷰 액시오스가 뷰 리소스보다 사용성이 좋다는 것을 증명해준다.


