# Spring AOP

### What is Spring AOP
> Aspect-oriented Programming (AOP) complements Object-oriented Programming (OOP) by providing another way of thinking about program structure. The key unit of modularity in OOP is the class, whereas in AOP the unit of modularity is the aspect. Aspects enable the modularization of concerns (such as transaction management) that cut across multiple types and objects. (Such concerns are often termed "crosscutting" concerns in AOP literature.)
- 관점 지향 프로그래밍
- OOP 모듈화 단위 = Class vs AOP 모듈화 단위= Aspect
- 횡단 관심사(cross-cutting concern)를 핵심 로직에서 분리하여 모듈성을 증가시키기 위함!
  - 로깅, 보안, 트랜젝션 관리 등과 같은 공통적인 관심사를 모듈화 ➡️ 코드 중복 줄이고 유지 보수성 향상에 도움

<br><br>


#### Core Concern vs Cross-cutting Concern

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

---

# Reference
토비의 스프링 vol1. 6장
https://docs.spring.io/spring-framework/reference/core/aop.html 와 그 하위문서
https://f-lab.kr/insight/understanding-spring-aop-and-proxy?gad_source=2&gclid=EAIaIQobChMIqOOemYychgMVzsdMAh0RBQ2wEAAYASAAEgKiIvD_BwE
https://adjh54.tistory.com/133