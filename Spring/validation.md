# 검증(Validation)

* `컨트롤러`의 중요한 역할은 http 요청이 정상적인지 검증
  * 클라이언트 검증은 조작할 수 있으므로 보안에 취약
  * 서버 검정은 고객 사용성이 부족
  * 둘 다, 필요
## 검증 처리
1. GET방식으로 등록 폼을 요청
2. 클라이언트에서 데이터를 입력하고 포스트방식으로 요청
3. 데이터 형식이 올바르지 않음(`검증 실패`)
4. 모델에 데이터를 담고 다시 폼을 포워딩

## FieldError, ObjectError
* FieldEroor
  * 특정 필드에서 발생한 에러를 담아두는 객체
  * 생성
    * objectName : Model의 어트리뷰트명
    * field : 해당 필드명
    * rejectedValue : 검증에 실패한 값
    * bindingFailure : 바인딩 실패여부
    * codes : 메시지 관리 파일에 메세지 코드명
    * arguments : 위 codes에서 사용하는 아규먼트
    * defualtMessage : 디폴트 메세지
```java
new FieldError(String objectName, String field, String defaultMessage);

new FieldError(String objectName, String field, @Nullable Object
rejectedValue, boolean bindingFailure, @Nullable String[] codes, @Nullable
Object[] arguments, @Nullable String defaultMessage)
```
* ObjectError
  * 필드 이외에 오브젝트 안에서 글로벌한 에러를 담아두는 객체
  * 생성
```java
new ObjectError(String objectName, String defaultMessage);

new ObjectError(String objectName, @Nullable String[] codes, @Nullable
Object[] arguments, @Nullable String defaultMessage)
```
* FieldError는 ObjectError를 상속

## BindingResult
* 검증 실패 시 에러의 데이터와 내용을 보관한는 스프링 객체
* `컨트롤러`메소드에서 파라미터 위치로 타겟이 되는 `@ModelAttribute`바로 뒤에 위치
* 특정 조건문 안에 `FieldError`나 `ObjectError`를 `.addError()`통하여 등록

  * 이 상태로 `.hasError()`를 써서 bindingResult의 에러가 있는지 확인 후 다시 폼페이지를 포워딩하면 에러메세지와 잘못 입력된 값이 담겨서 넘어감
```java
@Controller
public String form(
    @ModelAttribute("hospital") HospitalForm form,
    BindingResult bindingResult
) {
    if (필드나 오브젝트의 조건) {
        bindingResult.addError(new FieldError("hospital", "hospitalName", form.gethospitalName(), false, null, null, "병원 이름 필드 에러"))
    }
}
```
#### .rejectValue()
#### .reject()
* 타겟이 되는 `@ModelAttribue`에 대해 오류를 FieldError, ObjectError 직접 생성하지 않고 관리
* 매개변수
  * field : 해당 필드
  * errorCode : `MessageCodesResolver`가 인식할 에러코드
  * errorArgs : 메세지에 들어갈 아규먼트
  * defaultMessage : 디폴드 메세지
```java
@Controller
public String form(
    @ModelAttribute("hospital") HospitalForm form,
    BindingResult bindingResult
) {
    if (필드나 오브젝트의 조건) {
        bindingResult.rejectValue("hospitalName", "NotBlank", null, "공백X");
    }
}
```

### MessageCodesResolver
* `DefaultMessageCodesResolver`인 기본 구현체가 보통 사용
* `rejectValue()`, `reject()`에서 메세지 코드를 생성
* ObjectError
  * 에러코드.객체명
  * 에러코드
* FieldError
  * 에러코드.객체명.필드명
  * 에러코드.필드명
  * 에러코드.필드타입
  * 에러코드
    * 에러코드 : 위에서 매개변수로 넣어준 errorCode
    * 객체명 : 바인딩되는 객체의 이름
    * 필드명 : 에러가 발생한 필드의 이름
    * 필드타입 : 바인딩하려는 필드의 타입


#### 오류코드 전략
* 구체적인 코드 &rarr; 덜 구체적인 코드의 우선 순위
```properties
required.member.name = 회원 이름 필수
required.name = 이름 필수
required.String = 문자 입력 필수
required = 필수 사항
```
* 모든 필드 에러에 대해 구체적으로 에러코드를 지정해놓을 수 없기 때문에, 범용성 있는 코드 또한 작성해 둠

### Validator

* 컨트롤러에서 검증 로직 부분의 코드를 분리하여 
* `Validator`를 구현한 클래스를 작성

```java
@Component
public class MemberValidator implements Validator {

    /* 해당 Validator가 적용가능한 Object인지 판별하기 위함 */
    @Override
    public boolean supports(Class<?> clazz) {
        return Member.class.isAssignableFrom(clazz);
    }

    @Override
    public void validate(Object target, Errors errors) {
        
        /* 타겟으로 전달받은 객체 다운캐스팅 */
        Member member = (Member) target;

        ValidationUtils.rejectIfEmptyOrWhitespace(errors, "itemName", "required");
        
        if (검증조건) {
            /*bindingResult는 errors의 자식*/
            errors.rejectValue("필드", "에러코드", new Object[]{아규먼트, ...}, null);
        }
    }
}
```
* 컨트롤러에 등록
1. DI를 통한 직접 호출

```java
@Controller
public class MemberController {
    
    @Autowired
    private final MemberValidator memberValidator;

    @PostMapping("/member/add")
    public String add(@ModelAttribute Member member, BindingResult bindingResult){
        //검증 실패 시, 다시 폼으로 포워딩
        if (bindingResult.hasErrors()) {
            return "member/addForm";
        }
        //성공했을 떄 로직
        retrun "redirect:/member";
    }
}
```
2. WebDataBinder를 통해서 Validator를 등록 &rarr; `@Validated`를 통해서 실행
```java
@Controller
public class MemberController {
    
   @InitBinder
    public void init(WebDataBinder dataBinder) {
        dataBinder.addValidators(memberValidator);
    }

    @PostMapping("/member/add")
    public String add(@Validated @ModelAttribute Member member, BindingResult bindingResult){
        //검증 실패 시, 다시 폼으로 포워딩
        if (bindingResult.hasErrors()) {
            return "member/addForm";
        }
        //성공했을 떄 로직
        retrun "redirect:/member";
    }
}
```

## Bean Validation
* Bean Validation 2.0(JSR-380)이라는 기술 표준
  * 제일 많이 사용하는 구현체 : 하이버네이트 Validator

* 의존관계 추가
  * 추가 시 스프링이 자동으로 `LocalValidatorFactoryBean`을 글로벌 Validaotr로 등록
```
implementation 'org.springframework.boot:spring-boot-starter-validation'
```


* 검증 어노테이션을 클래스에 적용 시킴

* 검증 어노테이션 종류
  * @NotNull : 널 허용 X
  * @NotBlank : 공백 허용 X
  * @Range(min = 1, max =100) : 1~100까지 값 허용
  * ...
  * [검증어노테이션 종류](https://docs.jboss.org/hibernate/stable/validator/reference/en-US/html_single/?v=8.0#validator-defineconstraints-spec)
    * javax.validation.constraints.... : 표준 인터페이스
    *  org.hibernate.validator.constraints.... : 하이버네이트 Validation(구현체)
```java
public class Member {

    @NotNull
    private Long id;

    @NotBlank
    private String name;

    @Range(min = 1, max = 100) 
    private int age;

}
```
### 검증
1. @ModelAttribute의 바인딩 시도
   1. 바인딩 실패 시, `typeMismatch` 검증 오류 발생
2. Bean Validation 적용
   1. 해당 클래스의 검증어노테이션을 토대로 검증
   2. 검증 후에 FieldError나 ObjectError에 오류 추가

## 에러 코드
* 에러코드
  * 에러코드 : 위에서 매개변수로 넣어준 errorCode
  * 객체명 : 바인딩되는 객체의 이름
  * 필드명 : 에러가 발생한 필드의 이름
  * 필드타입 : 바인딩하려는 필드의 타입


#### 오류코드 전략
* 구체적인 코드 &rarr; 덜 구체적인 코드의 우선 순위
```properties
NotNull.member.name = 회원 이름 필수
NotNull.name = 이름 필수
NotNull.String = 문자 입력 필수
NotNull = 필수 사항
```