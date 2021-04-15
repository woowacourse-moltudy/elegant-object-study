# 1.3 생성자에 코드를 넣지 않는다.

주 생성자는 객체 초기화 프로세스를 시작하는 유일한 장소이기 때문에 제공되는 인자들이 완전해야한다고 말합니다.
('안자에 손대지 말라')

```java
class Cash {
	private int dollars;
    
    Cash(String dlr) {
    	this.dollars = Integer.parseInt(dlr);	// 손댔음
	}
}
```

객체 초기화 시 코드가 없어야(code free)하고 인자를 건드려선 안됩니다.
필요하다면 인자를 다른 타입의 객체로 감싸거나, 가공하지 않은 형식으로 캡슐화해야 합니다.

```java
class Cash {
	private Number dollars;
	Cash(String dlr) {
		this.dollars = new StringAsInteger(dlr);
		// 실제 사용 시점까지 객체 변환 작업을 연기한다!
	}
}

class StringAsInteger implements Number {
	private String source;
	StringAsInteger(String src) {
		this.source = src;
	}

	int intValue() {
		return Integer.parse(this.source);
	}
}
```

만약 첫번째 예제와 같은 경우로 사용하게 된다면,
객체를 만들 때마다 파싱이 수행되기 때문에 실행 여부를 제어할 수 없습니다.
반대로 인자가 전달된 상태 그대로 캡슐화하고 나중에 요청이 있을 경우 파싱하도록 하면, 클래스 사용자들이 파싱 시점을 자유롭게 결정할 수 있습니다.

물론 파싱이 단 한번만 수행되는 경우도 있을 것입니다.
하지만 '일관성'이라는 측면에서 미래에 어떤 기능이 추가될 지 모르기에, 미래의 리팩토링을 위해서 필요합니다.
결국 요지는 가벼운 생성자는 설정하기 쉽고 투명하게 사용할 수 있다는 것입니다.

# 느낀점

마지막 문장을 보면서 저게 가벼워진건가?라는 생각도 들었다.
오히려 CashNumber를 Number로 포장하는 것을 보면서 포장지를 두겹으로 싸는 느낌이 들었다.
그리고 CashNumber에 로직이 들어가면 그때마다 intValue() 호출해서 파싱해야하는 것에도 의문점이 생겼다.
너무 객체지향적으로 생각하는 것은 오히려 독이 될 수도 있지 않을까? (아니면 예시가 적절하다고 보기 어려울 수도 있겠다.)

