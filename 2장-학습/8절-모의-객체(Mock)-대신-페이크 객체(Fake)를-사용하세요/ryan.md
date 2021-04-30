## 모의 객체 대신 페이크 객체를 사용하세요

- 모킹 == 모의객체
- 객체를 잘 설계한다면 모킹이 필요하지 않다.
- 모킹은 실제 구현이 틀려지면, 정상 작동 하지만 테스트는 실패할 가능성이 있다. (유지보수성이 떨어짐)
- 인터페이스에 페이크 클래스를 넣어서 테스트하여라!

```java
interface Exchange {
	float rate(String target);
	float rate(String origin, String target);
 	final class Fake implements Exchange {
		@Override
		float rate(String target) {
			return this.rate("USD", target);
		}
		
		@Override
		float rate(String origin, String target) {
			return 1.2345;
		}
	}
}
```