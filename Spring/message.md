# message
* `메세지`를 다양한 곳에서 활용하기 위해 미리 등록해 두는 것
* 스프링에서 메세지 관리를 제공하는 `MessageSource` 인터페이스 활용

1.  메세지 관리 파일
```properties
#messages.properties
pet=반려동물
pet.id=반려동물 ID
pet.name=반려동물 이름
pet.age=반려동물 나이
```
2. `MessageSource`의 구현체(`ResourceBundleMessageSource`)를 스프링 빈으로 등록
    * 스프링 부트 사용 시, `spring.messages.basename=messages,config.188n.messages` 메세지 소스 설정
    * 
```java
@Bean
public MessageSource messageSource() {
    ResourceBundleMessageSource messageSource = new ResourceBundleMessageSource();

    //메세지 관리 파일의 이름을 등록
    messageSource.setBasenames("messages", "errors");

    //인코딩 정보 지정
    messageSource.setDefaultEncoding("utf-8");
    return messageSource;
}
```
3. 스프링 부트에서 basename은 messages가 기본 값

### 사용
* 메세지 관리 파일 등록
```properties
# messages.properties
pet=반려동물
pet.id=반려동물 ID
# {0}으로 매개변수 줄 수 있음
pet.name=반려동물 이름 {0}
pet.age=반려동물 나이 {0}
```
* MessageSource 등록
  * 메세지가 없으면 `NoSuchMessageException`예외 발생
```java
public class MessageSourceTest {
    @Autowired
    MessageSource ms;

    void helloMessage() {
        String result1 = ms.getMessage("pet", null, null);
        System.out.println(result1); //반려동물

        String result1 = ms.getMessage("pet.name", "두부", null);
        System.out.println(result1); //반려동물 이름 두부
    }
}
```
* 타임리프에서 사용
```html
<p th:text="#{pet}"></p>
<p th:text="#{pet.id}"></p>
<p th:text="#{pet.name(${'두부'})}"></p>
<p th:text="#{pet.age(${'5'})}"></p>

<p>반려동물</p>
<p>반려동물 ID</p>
<p>반려동물 이름 두부</p>
<p>반려동물 나이 5</p>
```

### 국제화
* 설정한 메세지를 나라, 언어 별로 관리하는 것
  * `messages.properties` 가 기본
  * `messages_en.properties`와 같이 여러 언어 관리 파일을 등록할 수 있음
    * 영어 사용자가 접근하면 messages_en에서 메세지를 가져옴
    * 그 외는 기본 설정 파일에서 가져옴

```properties
#messages_en.properties
pet=pet
pet.id=pet ID
pet.name=pet name
pet.age=pet age
```
* `LocaleResolver`의 구현체들을 통하여 `Locale` 선택
  * `AcceptHeaderLocaleResolver`
    * 클라이언트가 보내는 요청 헤더의 `Accept-Language`통하여 설정
```html
<p th:text="#{pet}"></p>
<p th:text="#{pet.id}"></p>
<p th:text="#{pet.name(${'두부'})}"></p>
<p th:text="#{pet.age(${'5'})}"></p>

<p>pet</p>
<p>pet ID</p>
<p>pet name 두부</p>
<p>pet age 5</p>
```

