# 예외 처리와 @ExceptionHandler

## Spring의 기본적인 예외처리

Spring은 만들어질 때(1.0)부터 에러 처리를 위한 BasicErrorController를 구현해두었고, 스프링 부트는 예외가 발생하면 기본적으로 **/error**로 에러 요청을 다시 전달하도록 WAS 설정을 해두었다.  
그래서 별도의 설정이 없다면 예외 발생 시에 **BasicErrorController**로 에러 처리 요청이 전달된다. 참고로 이는 스프링 부트의 WebMvcAutoConfiguration를 통해 자동 설정이 되는 WAS의 설정이다.

여기서 요청이 /error로 다시 전달된다는 부분에 주목해야 한다. 일반적인 요청 흐름은 다음과 같이 진행된다.

```
WAS(톰캣) -> 필터 -> 서블릿(디스패처 서블릿) -> 인터셉터 -> 컨트롤러
```

그리고 컨트롤러 하위에서 예외가 발생하였을 때, 별도의 예외 처리를 하지 않으면 WAS까지 에러가 전달된다. 그러면 WAS는 애플리케이션에서 처리를 못하는 예와라 exception이 올라왔다고 판단을 하고, 대응 작업을 진행한다.

```
컨트롤러(예외발생) -> 인터셉터 -> 서블릿(디스패처 서블릿) -> 필터 -> WAS(톰캣)
```

마지막으로 WAS는 스프링 부트가 등록한 에러 설정(/error)에 맞게 요청을 전달한다.

```
WAS(톰캣) -> 필터 -> 서블릿(디스패처 서블릿) -> 인터셉터 -> 컨트롤러
-> 컨트롤러(예외발생) -> 인터셉터 -> 서블릿(디스패처 서블릿) -> 필터 -> WAS(톰캣)
-> WAS(톰캣) -> 필터 -> 서블릿(디스패처 서블릿) -> 인터셉터 -> 컨트롤러(BasicErrorController)
```

## Spring이 제공하는 에러 처리 방법

### @ExceptionHandler

@ExceptionHandler는 매우 유연하게 에러를 처리할 수 있는 방법을 제공하는 기능이다. **@Controller, @RestController**가 적용된 Bean내에서 발생하는 예외를 잡아서 하나의 메서드에서 처리해주는 기능을 한다.

예를 들어 다음과 같이 컨트롤러의 메소드에 @ExceptionHandler를 추가함으로써 에러를 처리할 수 있다. @ExceptionHandler에 의해 발생한 예외는 ExceptionHandlerExceptionResolver에 의해 처리가 된다.

```java
@RestController
@RequiredArgsConstructor
public class ProductController {

  private final ProductService productService;

  @GetMapping("/product/{id}")
  public Response getProduct(@PathVariable String id){
    return productService.getProduct(id);
  }

  @ExceptionHandler(NoSuchElementFoundException.class)
  public ResponseEntity<String> handleNoSuchElementFoundException(NoSuchElementFoundException exception) {
    return ResponseEntity.status(HttpStatus.NOT_FOUND).body(exception.getMessage());
  }
}
```

@ExceptionHandler는 Exception 클래스들을 속성으로 받아 처리할 예외를 지정할 수 있다.  
위 예제에서 ProductController에 해당하는 Bean에서 NoSuchElementFoundException이 발생한다면, @ExceptionHandler(NoSuchElementFoundException.class)가 적용된 메서드가 호출될 것이다.

**장점:** ExceptionHandler는 @ResponseStatus와 달리 에러 응답(payload)을 자유롭게 다룰 수 있다는 점에서 유연하다.

**단점:** @ExceptionHandler는 컨트롤러에 구현하므로 특정 컨트롤러에서만 발생하는 예외만 처리된다. 하지만 컨트롤러에 에러 처리 코드가 섞이며, 에러 처리 코드가 중복될 가능성이 높다.

### @ControllerAdvice와 @RestControllerAdvice

Spring은 **전역적으로 @ExceptionHandler를 적용할 수 있는** @ControllerAdvice와 @RestControllerAdvice 어노테이션을 각각 Spring3.2, Spring4.3부터 제공하고 있다.
두 개의 차이는 @Controller와 RestController와 같이 @ResponseBody가 붙어 있어 응답을 Json으로 내려준다는 점에서 다르다.

```java
@RestControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(NoSuchElementFoundException.class)
    protected ResponseEntity<?> handleNoSuchElementFoundException(NoSuchElementFoundException e) {
        final ErrorResponse errorResponse = ErrorResponse.builder()
                .code("Item Not Found")
                .message(e.getMessage()).build();

        return ResponseEntity.status(HttpStatus.NOT_FOUND).body(errorResponse);
    }
}
```

**장점:**

- 하나의 클래스로 모든 컨트롤러에 대해 전역적으로 예외 처리가 가능함

- 직접 정의한 에러 응답을 일관성있게 클라이언트에게 내려줄 수 있음
- 별도의 try-catch문이 없어 코드의 가독성이 높아짐

## 예상 질문

- 스프링은 기본적으로 어떻게 예외를 처리하나요?
- @ExceptionHandler와 @ControllerAdvice의 특징을 간단히 설명해 주세요.

## 참고 링크

https://mangkyu.tistory.com/204
