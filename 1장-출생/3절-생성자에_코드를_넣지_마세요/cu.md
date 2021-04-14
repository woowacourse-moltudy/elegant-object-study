# 1.3 생성자에 코드를 넣지 마세요

- 인자에 손대지 말라! 인자를 직접 변환하려 하지말고, 객체를 조합하라

```java
class Cash {
	private int dollars;
	Cash(int dollars) {
		this.dollars = Integer.parseInt(dollars);
	}
}
```
```java
class Cash {
	private Number dollars;
	Cash(int dollars) {
		this.dollars = new StringAsInteger(dollars);
	}
}
```

- 단순히 파싱하는 정도는 Cash의 다양한 생성자를 통해 해결해도 되지 않을까? 너무 많은 객체의 조합이 비즈니스 로직을 이해하는데 저해를 주진 않을까?
- Lazy Loading의 이점과 데코레이터 패턴의 이점은 공감이 가나, 여기서 예로 제시한 캐싱전략에서 Lazy Loading이 갖는 이점은 공감하기 어렵다. 
