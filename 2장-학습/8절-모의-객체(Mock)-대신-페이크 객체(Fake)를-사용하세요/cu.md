# 2.8 모의 객체(Mock) 대신 페이크 객치(Fake)를 사용하세요

- Fake 객체를 사용하면 Mock 객체를 사용하는 것보다 가독성에서 이점이 있다.
- Mock 객체는 가정을 사실로 전환시키기 때문에 단위 테스트를 유지보수하기 어렵다.
  Mock 객체는 특정 메서드를 호출하리라고 "가정"하는데, 이는 객체의 구현방법을 알고 있다고 가정하는 것이다.
  그러다보니 단위테스트하려는 대상의 행동이 변하지 않았는데도, 가정했던 도메인의 변화로 테스트코드가 깨질 수 있다.
  단위 테스트를 클래스의 일부로 보는 시각에서 이는 OCP 원칙 위반으로 캡슐화가 깨졌음을 의미한다.
- 협력 객체의 변화로 단위테스트를 수정해야 한다면 리팩토링 비용이 증가한다.
- 인터페이스 설계를 더 깊이 고민하도록 만든다.

### 느낀 점

- 끝나지 않을 classicist vs mockist : classicist 는 상태 검증이 목적이고, mockist는 행위 검증이 목적이다.

#### * classicist
- 저자의 경우 객체의 자율을 존중하는 쪽이라 classicist인듯 하다. classicist는 가능한 실제 객체를 사용하고 객체간의 협력으로 복잡한 케이스일 경우, 테스트 더블을 사용한다.

- 테스트 더블이란, 테스트 목적으로 실제 객체 대신 사용되는 모든 종류의 가짜 객체를 의미한다. 테스트 더블에는 stub, mock, fake , spy 등이 있다. classicist 는 이 중 stub 혹은 fake 객체를 사용한다.

> https://martinfowler.com/articles/mocksArentStubs.html

- fake 와 stub은 다시 봐도 헷갈린다. fake 객체는 실제로 Production에는 사용하지 않고 간단한 기능만을 제공하는 객체를 의미하고, stub이란 미리 지정된 답변으로 응답하는 것을 의미한다고 설명이 되어 있다. 그럼 생각해보면, 아래와 같아야 할텐데 예제코드는 반대로다. 왜 MailServiceStub인지 설명 좀..

```sh
public class MenuFake implements Menu {
    private static final List<Menu> menus = new ArrayList<>();

    static {
        menus.add(new Menu(1, "후라이드", Category.CHICKEN, 16_000));
        menus.add(new Menu(2, "양념치킨", Category.CHICKEN, 16_000));
    }

    public static List<Menu> menus() {
        return Collections.unmodifiableList(menus);
    }
}
```

```sh
	@Override
	float rate(String origin, String target) {
		return 1.2345;
	}
```

#### * mockist
- mockist(bdd(given-when-then)도 mockist의 분파)는 mock에 대한 측을 명세하고 테스트를 시작한다. 협력객체들의 행동을 예측해두어 계층적(layered)인 구조에서도 잘 동작한다. 객체에 메시지를 던지고 그 응답만을 테스트하고 인접한 Mock들을 작성하므로 복잡한 픽스쳐를 구성할 필요도 없고, 테스트를 고립시킬 수 있다.
- 지금껏 일하면서 테스트 시나리오를 작성하기 용이해서 given-when-then 패턴을 활용해왔고 행위 검증의 테스트가 의도를 분명히 드러낸다고 생각해왔다. 하지만, stubbing을 할 경우, 협력하는 객체의 Public Operation이 변경할 경우 바로 감지가 가능하나, mockist의 방식은 감지하기 어려울 수 있다. 테스트에서의 예측이 잘못되었는데도 단위테스트 결과가 성공이라 버그를 내포할 수 있다. 
