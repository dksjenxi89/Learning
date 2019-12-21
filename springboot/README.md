## 백기선 개발자의 스프링부트 인프런 강좌 보며 정리!


### 모르거나 복습 정리!!
- maven 간에는 프로젝트 간을 계층 구조로 만들 수 있다.

- DI  방법 정리 => 1) 어노테이션, 2) Bean, 3) xml



### 어노테이션 정리!
@SpringBootApplication - @Configuration, @EnableAutoConfiguration, @ComponentScan 3가지를 디폴트 속성으로 사용하는 것고 같다.

SpringBoot는 편의를 위해 스프링부트어플리케이션 어노테이션을 제공한다.

스프링부트 개발자들은 메인 클래스의 @Configuration, @EnableAutoConfiguration, @ComponentScan를 어노테이트하고 시작하는데

그걸 위한 편의성을 위한 어노테이션인듯


@Configuration - @Configuration은 설정을 위한 어노테이션으로 개발자가 생성한 class를 Bean으로 생성 할 때 Single Tone으로 한번만 생성하는 것.

- 싱글톤 - 전역 변수를 사용하지 않고 객체를 하나만 생성 하도록 하며, 생성 된 객체를 어디에서든지 참조할 수 있도록 하는 것.

@EnableAutoConfiguration - 스프링 Application Context를 만들 때 자동으로 설정 하는 기능을 켠다. 
사용자가 필요할 것 같은 빈(bean)을 추측해서 ApplicationContext를 만들 때 필요한 설정을 한다. 클래스패스(classpath)를 기준으로 설정을 한다. 
예를들어 클래스패스에 tomcat-embeded.jar이 있으면 TomcatEmbeddedServletContainerFactory가 있을 것이라고 추측 해서 설정을 해준다.

@ComponentScan - 지정한 위치 이하에 있는 @Component와 @Configuration이 붙은 class를 스캔해서 Bean으로 등록한다.
스프링 XML 설정의 <context:component-scan>을 대신해서 자바에서 설정.

### 클래스 정리! 
- SpringApplication - 스프링어플리케이션 클래스는 스프링 어플리케이션을 구동하는 편리한 방법을 제공한다.
스프링 어플리케이션은 메인 메소드부터 시작할텐데 많은 상황에서 단순한 static한 SpringAppliction.run 메소드를 델리게이트할 수 있게 한다.
