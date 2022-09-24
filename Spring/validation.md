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

