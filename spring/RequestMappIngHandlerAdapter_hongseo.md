# RequestMapping Handler Adapter

## 개념정리

### HandlerAdapter(핸들러 어댑터) 정의

- Handler Mapping에서 찾은 특정 Controller(Handler)를 실행하기위해서는 핸들러 어댑터가 필요하다.
- 핸들러 어댑터는 컨트롤러로 요청을 위임한는 역할을 한다.
- 정확히 그 안에서 요청을 전/후 처리 과정을 담당한다.

### Handler Adapter를 사용하는 이유

- 다양한 방법으로 Controller(Handler)를 구현할 수 있다.
- 이러한 컨트롤러를 모두 처리하기 위해서 Handler Adapter를 사용한다.

### 다양한 방법으로 구현된 컨트롤러를 처리하는 방법

- Handler Adapter의 supports()로 해당 adapter가 handler 처리를 지원하는지 판단하기위해 순서대로 호출
  - 핸들러 어댑터는 다양한 컨트롤러를 지원

```java
0 = RequestMappingHandlerAdapter   // 애노테이션 기반의 컨트롤러인 @RequestMapping에서 사용
1 = HttpRequestHandlerAdapter      // HttpRequestHandler 처리
2 = SimpleControllerHandlerAdapter // Controller 인터페이스 처리
```

- 찾은 핸들러(컨트롤러)를 파라미터로 넘겨 HandlerAdapter를 가져와서 이를 통해 핸들러 호출한다.
- handler 메서드를 실행하면 위 메서드가 순차적으로 실행된다.

### RequestMappingHandlerAdapter의 처리과정

1. **@RequestMapping 어노테이션과 메소드 실행:**
   - RequestMappingHandlerAdapter는 _@RequestMapping_ 어노테이션이 달린 메소드를 실행하여 요청을 처리한다.
2. **ArgumentResolver를 통한 데이터 생성:**
   - RequestMappingHandlerAdapter는 요청을 받으면, 해당 요청에 필요한 데이터를 생성하기 위해 ArgumentResolver를 활용한다.
   - ArgumentResolver는 요청에 담긴 정보(예: HttpServletRequest, Model, @RequestParam, @ModelAttribute, @RequestBody, HttpEntity 등)를 기반으로 컨트롤러가 필요로 하는 데이터를 생성한다.
3. **값 전달 및 컨트롤러 처리:**
   - ArgumentResolver가 생성한 데이터는 RequestMappingHandlerAdapter가 컨트롤러에게 전달한다.
   - 컨트롤러는 이를 받아 비즈니스 로직을 수행하고, 그 결과 값을 반환한다.
4. **ReturnValueHandler를 통한 응답 처리:**
   - ReturnValueHandler는 컨트롤러가 반환한 값을 받아서 응답을 생성하고 변환한다.
   - 이 과정에서 컨트롤러의 반환 값이 HTTP 응답으로 변환되어 클라이언트에게 전달될 수 있도록 처리한다
5. **RequestMappingHandlerAdapter를 통한 값 전달:**
   - ReturnValueHandler가 처리한 값을 다시 RequestMappingHandlerAdapter에게 전달한다.
   - RequestMappingHandlerAdapter는 최종적으로 이 값을 사용하여 클라이언트에게 응답을 제공한다.

## 예상질문

- RequestMappingHandlerAdapter의 처리과정을 설명해주세요.
- Handler Adapter를 사용하는 이유는 무엇인가요?

---

### 참고자료

[https://velog.io/@jeongyunsung/스프링부트-해부학-Handler-Resolver](https://velog.io/@jeongyunsung/%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8-%ED%95%B4%EB%B6%80%ED%95%99-Handler-Resolver)

https://xonmin.tistory.com/9
