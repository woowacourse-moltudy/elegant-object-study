스마트 개념은 인터페이스에서 구현자에게 너무 많은 것을 요구하는 것을 방지하기 위한 방법이다. 이전, 페이크 객체와 마찬가지로 인터페이스 내에 스마트 객체를 생성해서 많은 메서드 구현 방식을 줄이는 것이다.

```java
interface Exchange {
	float rate(String source, String target);
	final class Smart {
		private final Exchange origin;
		public float toUsd(String source) {
			return this.origin.rate(source, "USD");
		}
	}
}
```

데코레이터 패턴과 매우 유사하다! 스마트 객체는 결국 인터페이스를 짧게 유지하기 위한 객체이므로 인터페이스를 짧게 유지해야한다는 목적을 기억하자!