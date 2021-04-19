# 2.5 퍼블릭 상수를 사용하지 마세요

- 퍼블릭 상수마다 계약의 의미를 캡슐화하는 새로운 클래스를 만들어야 한다고?! 그리고 method chaining에 리터럴을 사용하는 것 보다 클래스 중첩이 더 좋다고?

```java
new HttpRequest().method(POST);
new PostRequest(new HttpRequest());
```

- 값을 하드코딩하기보다는 도메인 내에서 사용하도록 private 상수를 두면 되지 않은가?
- URL의 경우 Controller에서의 중복을 제거하는 것 외에도 테스트코드에서도 재사용할 수 있어 실용적인데 URL도 별도의 클래스로 작성하라는 말인가?
