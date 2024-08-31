
  ## 특징
  * Node.js 서버 애플리케이션을 구축하기 위한 프레임워크
  * Express 기반
  * Typescript 사용
  * OOP, FP, FRP 등의 프로그래밍 패러다임을 지원
  * unit test, e2e test 지원


  ## 배경
  node.js의 높은 자유도로 인해 아키텍처 구성이 어렵고 효과적이지 않았음
  그래서 Angular의 아키텍처를 참고하여 Nest.js를 만듬


  ## 장점
  * Angular와 비슷한 구조
  * Typescript 사용
  * 아키텍처 구성이 쉬움
  * 라우팅, 보안 등의 기능을 제공


  ## 구조
  * 각 응용 프로그램에는 하나 이상의 모듈, 즉 Root Module이 존재
  * Module은 Controller, Provider로 구성
  * Controller는 요청을 받아 처리하고, Provider는 비즈니스 로직을 처리
  * Module은 다른 Module을 import할 수 있음
  * 예시
    1. 클라이언트가 요청
    2. Controller가 요청을 받아 Provider에게 전달
    3. Provider는 비즈니스 로직을 처리한 후 결과를 Controller에게 전달
    4. Controller는 결과를 클라이언트에게 전달


  ## Controller
  * 요청을 받아 처리하는 클래스
  * Nest Runtime에 의해 관리되며, 의존성 주입을 통해 다른 Provider를 사용할 수 있음
  * Express의 Router와 비슷한 역할을 함
  * 데코레이터를 사용하여 라우팅을 설정할 수 있음

  ## Provider
  * 비즈니스 로직을 처리하는 클래스
  * Service, Repository, Factory, Helper 등으로 구성
  * Nest Runtime에 의해 관리되며, 의존성 주입을 통해 다른 Provider를 사용할 수 있음

  ## Middleware
  * 요청과 응답 사이에서 실행되는 함수
  * 인증, 로깅, 예외 처리 등의 기능을 수행
