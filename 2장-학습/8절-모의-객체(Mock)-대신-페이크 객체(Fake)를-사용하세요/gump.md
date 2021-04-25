## 2.8-모의-객체(Mock)-대신-페이크 객체(Fake)를-사용하세요

## 정리

### 모킹은 나쁜 프랙티스이며 최후의 수단으로만 사용해야해요

모킹 대신 '페이크 객체(fake object)'를 사용해요.

```java
interface Exchange {
    float rate(String origin, String target);
    final class Fake implements Exchange {
        @Override
        public float rate(String origin, String target) {
            return 1.2345f;
        }
    }
}
```

이를 이용한 단위테스트 아래와 같아요.

```java
Exchange exchange = new Exchange.Fake();
Cash dollar = new Cash(exchange, 500);
Cash euro = dollar.in("EUR");
assert "6.17".equals(euro.toString());
```

단위테스트가 훨씬 짧아진 것을 확인할 수 있어요.

### '페이크(Fake)'클래스는 강력해져야 하고 '실제' 클래스보다 더 복잡해지는 경우도 있어요

페이크 클래스를 만족하도록 테스트를 작성하지 말고, 페이크 클래스가 테스트를 올바르게 지원하도록 만들어야해요.

페이크 클래스를 사용하면 테스트를 더 짧게 만들 수 있기 때문에 유지보수성이 눈에 띄게 향상되요.

### 모킹은 가정을 사실로 전환시키기 띠문애 단위 테스트를 유지보수하게 어렵게 만들어요

클래스의 공개된(public) 행동을 변경하지 않을 경우 **단위 테스트는 실패해서 안돼요**. 즉, 단위 테스트는 거짓 양성 지표를 제공해서는 안돼요. 

하지만 모킹은 가정을 사실로 만들기 때문에, 아무런 이유 없이도 실패할 수 있어요. 

### 모킹의 문제 예시

```java
interface Exchange {
    float rate(String target);
    float rate(String origin, String target);
}
```

요구사항이 추가되어, 한 개의 인자를 받는 메서드를 추가 했다면, 실제 코드에서는 아무런 문제가 없지만 테스트 코드에서 에러가 발생할 수 있어요. (클래스는 여전히 잘 동작하지만, 테스트는 실패해요)

### 페이크를 쓴다면

```java
interface Exchange {
    float rate(String target);
    float rate(String origin, String target);
    final class Fake implements Exchange {
        @Override
        public float rate(String target) {
            return this.rate("USD", target);
        }

        @Override
        public float rate(String origin, String target) {
            return 1.2345f;
        }
    }
}
```

페이크 클래스가 존재하는 상황에서 Exchange 인터페이스를 변경하기 위해서는 자연스럽게 Exchage.Fake 클래스의 구현도 함께 변경해요.

이때는, 단위테스트를 변경할 필요가 없어요. 

### 모킹은 단위 테스트를 지원하기 위해 만들어졌지만 실제로는 단위 테스트에 우호적이지 않아요.

모킹은 클래스 구현과 관련된 내부의 세부사항을 테스트와 결합시켜요.

### 반대로 페이크 객체를 사용하면 테스트를 충분히 유지보수 가능하게 만들 수 있어요. Cash 클래스와 Exchange 클래스 사이의 의사소통 방식에 대해서는 신경 쓸 필요가 없기 때문이에요.

우리가 Exchange 인스턴스를 Cash에게 제공하기 때문에, Cash가 Exchange를 사용하는 방법에 대해 알 권리가 우리에게 있다고 생각할수 있어요. 하지만 우리에게 객체의 구현 방법을 알 권리는 없어요. 테스트가 객체 내부의 구현 세부사항을 알면 테스트가 취약해지고 유지보수하기도 어려워져요.

### 페이크 클래스는 인터페이스의 설계에 관해 더 깊이 고민하도록 해줘요

인터페이스를 설계하면서 '페이크'클래스를 만들다보면 필연적으로 인터페이스의 작성자뿐만 아니라 사용자의 관점에서도 고민하게 해줘요. 인터페이스를 다른 각도에서 바라보고, '테스트'리소스를 사용해서 사용자와 동일한 기능을 구현해요 

## 의견

Mock 방식이 단위테스트를 위해 필연적으로 필요한 기술이라 생각했어요. 

인터페이스에 Fake클래스를 추가하면, Mock을 쓰지 않아도 단위 테스트를 진행할 수 있다는 것이 신기해요.

아직 Fake클래스가 어색하지만, 다음 미션때 적용해보려 해요.