```java
class Cash {
	private final int dollars;
	public Cash mul(int factor) {
		return new Cash(this.dollars * factor);
	}
}
```

위와 같이 상태를 변경한다면 새로운 객체를 생성해서 반환하는 것을 불변 객체라고 한다. 그 반대, 즉, 상태만 변경되는 객체를 가변 객체라 한다. 가변객체로 만들게 되면 예상치 못한 결과를 발견할 수도 있다. (모르는 곳에서 값 변경이 일어날 경우) 그렇다면 불변객체를 사용하게 된다면 어떤 장점이 있을까?

- **식별자 가변성 문제가 없다.**
- **실패 원자성**

  실패 원자성이란 완전하고 견고한 상태의 객체를 가지거나 아니면 실패하거나 둘 중 하나만 가능한 특성이다. 가변객체경우 상태를 변경하다 에러가 발생한다면 내부의 어떤 것은 변경이 되어 있고 어떤 것은 변경에 실패하게 된다. 실패 원자성이 보장되지 않는다는 것이다.

- **시간적 결합을 제거할 수 있다.**

  만일 가변객체를 사용하여 먼저 객체를 생성하고 필드를 채워나가는 방식으로 가게 되면 중간 실행 순서가 꼬일 수도 있다. 하지만 불변 객체라면 이러한 결합을 제거할 수 있다.

- **부수효과 제거**

  중간 실수를 하더라도 원래 객체에는 영향이 없기 때문에 부수적인 효과가 없다.

- **NULL 참조 없애기**

  null을 이용한 코드는 항상 피해야한다. 그리고 최대한 null 값을 소유하지 않도록 노력해야 한다. 처음 만들 때 완벽한 객체를 만드는게 좋다.

- **스레드 안전성**

  웹, 빅 데이터 등으로 인해 멀티 스레드 환경에서의 안전성은 매우 중요하다. 만일 가변 객체라면 멀티 스레드 환경에서의 안전성을 보장할 수 없다.

- **더 작고 더 단순한 객체**

  불변 객체를 만드려 하면 처음부터 완벽한 객체를 만들려고 노력한다. 그러다보니 생성자에 인자를 받는데 인자 수가 많아진다면 무언가 잘못된 것을 알고 계속 분리하려고 노력할 것이다. 자연스레 더 작고 더 단순한 객체가 탄생할 것이다.

불변 객체로만 만드려고 하면 한계점도 있다. 예를 들어, 지연 로딩을 사용하기가 힘들다. 최근 객체를 불변으로 유지하면서도 지연 로딩을 구현할 수 있는 다양한 해결방법이 나온다.

### 느낀점

불변 객체는 버그가 생길 수 있는 원천을 아예 없애버리는 것 같다.

물론, 계속해서 생기는 객체 때문에 메모리 면에서는 손해가 있겠지만 캐싱과 같은 기술을 사용할 수 있으니! 그리고 GC를 믿자!!

하지만 아쉬운 건 역시 외부 라이브러리와의 호환성인 것 같다. 현재 자바 진영에서는 JPA 기술을 이용해 도메인 주도 개발이 가장 핫한 것 같다. 하지만 JPA특성 상(영속성 컨텍스트를 이용한 더티체킹) 엔티티를 가변 객체로 만들어야하는 것으로 알고 있다. 이러한 점 때문에 실제 서비스에서는 적용하기 힘든 규칙이지만 충분히 변화가 일어나야 한다고 생각한다!

JPA를 사용할 때 엔티티를 불변객체로 사용해도 작동하게끔 컨트리뷰트를 하자!! 가즈아!!!!