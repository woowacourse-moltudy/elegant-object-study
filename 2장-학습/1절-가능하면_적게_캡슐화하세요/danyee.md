# 2.1 가능하면 적게 캡슐화하세요

## 정리
- 한 클래스는 최대 4개의 객체를 캡슐화해야 한다.
    - 이를 초과하면 해당 클래스는 완전히 잘못된 방식으로 구현된 것이다.
- 클래스 내부에 캡슐화된 객체 전체를 가리켜 객체의 상태(state) 또는 식별자(identity)라고 부른다.
<br/>

```
class Cash {
    private Integer digits;
    private Integer cents;
    private String currency;
}
```
- Cash 클래스는 3개의 객체를 캡슐화하고 있다.
    - 이 3개의 객체들이 함께 모여 Cash 클래스의 객체를 식별한다.
    - 동일한 값의 달러, 센트, 통화를 캡슐화하는 Cash 클래스의 두 객체는 서로 동일하다(same).
<br/>

```
Cash x = new Cash(29, 95, "Cash");
Cash y = new Cash(29, 95, "Cash");
assert x.equals(y);
assert x == y;
```
- 객체 패러다임에서는 두 객체 x, y가 동일하다고 판단하는 반면, Java에서는 동일하지 않다고 판단한다.
    - 이는 Java 언어가 안고 있는 설계적 결함 때문이다.
    - 두 객체 x, y의 상태는 동일하지만 식별자는 서로 다르다.
- Java 언어의 결함을 해결하기 위해 항상 `equals()` 메소드를 오버라이드해야 한다.
    - Lombok 프로젝트에서 제공하는 `@EqualsAndHashCode` 어노테이션을 사용해도 된다.

## 느낀점

- 클래스를 작게 유지해야 한다는 저자의 의견에 동의한다.
    - 체스 미션에서는 이를 제대로 못 지킨 것 같다. 시간이 되면 리팩토링하면서 고쳐봐야지.
- `equals()`, `hashCode()` 메소드 대신 `@EqualsAndHashCode` 어노테이션을 사용할 수 있다는 걸 처음 알았다. 다음에 한번 써봐야겠다!