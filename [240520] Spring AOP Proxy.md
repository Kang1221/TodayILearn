# Spring AOP Proxy


### What is Spring AOP
> Aspect-oriented Programming (AOP) complements Object-oriented Programming (OOP) by providing another way of thinking about program structure. The key unit of modularity in OOP is the class, whereas in AOP the unit of modularity is the aspect. Aspects enable the modularization of concerns (such as transaction management) that cut across multiple types and objects. (Such concerns are often termed "crosscutting" concerns in AOP literature.)
- 관점 지향 프로그래밍
- OOP 모듈화 단위 = Class vs AOP 모듈화 단위= Aspect
- 횡단 관심사(cross-cutting concern)를 핵심 로직에서 분리하여 모듈성을 증가시키기 위함!
  - 로깅, 보안, 트랜젝션 관리 등과 같은 공통적인 관심사를 모듈화 ➡️ 코드 중복 줄이고 유지 보수성 향상에 도움

<br>

#### ** 참고

Core Concern 
- 핵심 관심사
- 각 객체가 가져야 할 본래의 기능

Cross-cutting Concern
- 공통 관심사/횡단 관심사
- 여러 객체에서 공통적으로 사용되는 코드

<br>
<br>


### AOP is used in the Spring Framework to:
> 1. Provide declarative enterprise services.
  <br>The most important such service is declarative transaction management.<br><br>
> 2. Let users implement **custom aspects**, complementing their use of OOP with AOP.


<br>
<br>

# Spring AOP Proxy
위에서 설명한 Spring AOP를 구현하는 기술 중 하나.
대상 객체에 대한 접근을 제어, 추가 기능을 수행하기 위해 사용됨.
(프록시로 실체 객체를 감싸면, 클라이언트가 실제 객체인지 프록시 객체인지 모르게하면서 추가적인 기능을 제공할 수 있기 때문 )


## 다이나믹 프록시 & CGLIB
스프링 AOP에서 주로 사용되는 프록시 기술

###  다이나믹 프록시
> Spring AOP defaults to using standard JDK dynamic proxies for AOP proxies. 
This enables any interface (or set of interfaces) to be proxied.
- java.lang.reflect.Proxy 클래스를 사용하여 인터페이스 기반의 프록시 객체를 동적으로 생성
- 인터페이스를 통해 동적으로 프록시 객체를 생성하고 관리할 수 있기 때문

### CGLIB
> Spring AOP can also use CGLIB proxies. This is necessary to proxy classes rather than interfaces. By default, CGLIB is used if a business object does not implement an interface. As it is good practice to program to interfaces rather than classes, business classes normally implement one or more business interfaces. It is possible to force the use of CGLIB, in those (hopefully rare) cases where you need to advise a method that is not declared on an interface or where you need to pass a proxied object to a method as a concrete type.
- CGLIB(Code Generation Library)는 인터페이스가 없는 클래스를 상속받아 프록시 객체를 생성할 수 있는 기술
- 바이트코드 조작을 통해 실제 클래스를 상속받은 프록시 객체를 생성하기 때문

<br>
<br>

## 스프링 AOP의 작동 원리
!! 스프링 AOP는 프록시 패턴을 기반으로 동작 
- 즉, 클라이언트가 객체를 사용할 때, 스프링 컨테이너는 대상 객체 대신 프록시 객체를 제공
이를 통해 메소드 호출 전후에 추가적인 기능을 수행할 수 있기 때문

- 이 과정에서 AspectJ 표현식을 사용하여 어떤 메소드에 어드바이스(추가 기능)를 적용할지 결정
- 프록시 객체는 실제 객체의 메소드를 호출하는 동시에, AOP가 적용된 특정 포인트에서 사용자 정의 코드를 실행합니다.
 이 방식을 통해 개발자는 비즈니스 로직과 공통 기능을 분리하여 관리할 수 있기 때문

<br>
<br>

---

# Reference
토비의 스프링 vol1. 6장
https://docs.spring.io/spring-framework/reference/core/aop.html 와 그 하위문서
https://f-lab.kr/insight/understanding-spring-aop-and-proxy?gad_source=2&gclid=EAIaIQobChMIqOOemYychgMVzsdMAh0RBQ2wEAAYASAAEgKiIvD_BwE
https://adjh54.tistory.com/133