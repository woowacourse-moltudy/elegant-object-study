## 정리

**인자에 손대지 말라!** 이 장의 핵심 문장이다.

객체 초기화 단계에선 코드가 없어야하고 인자를 건드려선 안된다. 그렇다면 어떻게 각기 다른 타입을 인자로 전달 받을 수 있을까? **다형성**을 이용하자! 타입을 한 번 감싸 감싼 타입을 필드로 올려놓는 것이다.

```java
class Cash {
	private Number dollars;
	Cash(String dlr) {
		this.dollars = new StringAsInteger(dlr);
	}
}

class StringAsInteger implements Number {
	private String source;
	StringAsInteger(String src) {
		this.source = src;
	}
	int intValue() {
		return Integer.parseInt(this.source);
	}
}
```

여기서 핵심은 객체를 초기화하는 시점에 곧장 텍스트를 숫자로 변경하는 것이 아니라 실제로 사용하는 시점까지 객체의 변환 작업을 연기한다는 것이다.

그렇다면 의문이 든다. 실제로 사용할 때마다 변환 작업이 이뤄지면 성능이 안 좋은 것 아닌가? 이에 대한 해결책은 **데코레이터 패턴**이다.

```java
class CachedNumber implements Number {
	private Number origin;
	private Collection<Integer> cached = new ArrayList<>(1);

	public CachedNumber(Number num) {
		this.origin = num;
	}

	public int intValue() {
		if (this.cached.isEmpty()) {
			this.cached.add(this.origin.intValue());
		}
		return this.cached.get(0);
	}
}

Number num = new CachedNumber(new StringAsInteger("123"));
```

이 방법으로 인해 객체를 인스턴스화하는 동안에는 객체를 만드는 일 이외에는 어떤 일도 수행하지 않는다.

## 느낀점

새로운 인사이트를 준 챕터였다. 생성자에 코드를 넣지 않기 위해 다형성을 이용해 많은 타입을 받을 수 있게 하는 생성자! 이 덕분에 사용이 가능해진 많은 기법(lazy, caching)!!

스프링 웹소켓을 사용할 때 Message 인터페이스 관련 api를 사용할 때 이러한 생성자에 다형성을 사용했던 것 같다. 하지만 api를 사용하는 입장에서는 좀 불편했다. 인터페이스의 구현체를 일일이 찾아보고 이 구현체가 `String` 을 받는 지 `Integer` 를 받는 지 찾기가 너무 불편했던 것이다.

만일 모든 객체에 이러한 룰을 지키게 된다면 api를 사용하는 입장에서 많이 불편할 것이다. 그러기에 복잡한 로직이나 무거운 로직이 아니라면 적절히 생성자에서 인자를 건드려도 괜찮지 않을까?