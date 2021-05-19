# 충성스러우면서 불변이거나, 아니면 상수이거나



## 상태와 데이터

- 객체가 살아있는 동안 상태가 변하지 않는다.

```JAva
class WebPage {
	private final URI uri;
	
	WebPage(URI path) {
		this.uri = path;
	}
	
	public STring content() {
		// HTTP GET 요청을 전송해서,
		// 웹 페이지의 컨테르를 읽은 후,
		// 읽혀진 컨텐츠를 UTF-8 문자열로 변환한다.
	}
}
```



- content()를 실행 할 때마다 다른 값이 반환되더라도, 위 객체는 불변이다.
  - 객체를 대표하는 엔티티에 충성하기 때문이다.
- 기본적으로 모든 객체는 식별자, 상태, 행동을 포함
- 불변 객체와 가변 객체의 중요한 차이는 불변 객체에는 식별자가 존재하지 않으며 절대로 상태를 변경할 수 없다는 점
  - 불변객체의 식별자는 객체의 상태와 완전히 동일하다.
- 동일한 URI를 가진 두 개의 WebPage 인스턴스는 content에서 항상 같은 값을 리턴한다.

# 느낀점

- 아직 잘 모르겠다..

- 아래 글을 한 번 더 읽어봤다.

- https://woowacourse.github.io/javable/post/2020-05-18-immutable-object/