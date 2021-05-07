# 2.8 모의 객체(Mock) 대신 페이크 객체(Fake)를 사용하세요

## 정리
- 모킹(mocking)은 bad practice이다. 👉 따라서, 페이크 객체(fake object)를 사용해야 한다.

```
// mocking
Exchange exchange = Mockito.mock(Exchange.class);
Mockito.doReturn(1.15)
    .when(exchange)
    .rate("USD", "EUR");
Cash dollar = new Cash(exchange, 500);
Cash euro = dollar.in("EUR");
assert "5.75".equals(euro.toString());

// fake object
interface Exchange {
    float rate(String origin, String target);

    final class Fake implements Exchange {
        @Override
        float rate(String origin, String target) {
            return 1.2345;
        }
    }
}

Exchange exchange = new Exchange.Fake();
Cash dollar = new Cash(exchange, 500);
Cash euro = dollar.in("EUR");
assert "6.17".equals(euro.tostring());
```

- 단위 테스트는 코드 리팩토링에 큰 도움이 된다. 👉 참 양성(true positive)
- 동시에 행동이 변경되지 않을 경우에는 실패해서는 안 된다. 👉 거짓 양성(false positive)
    - 클래스의 공개된(public) 행동을 변경하지 않을 경우 실패하면 안 된다.
- 모킹을 사용하면 단위 테스트가 너무 쉽게 깨지고 불안정해진다. 한편, 페이크 객체를 사용하면 단위 테스트가 훌륭하고 신뢰 가능해진다.
- 그러므로 모킹을 사용하지 말고, 항상 인터페이스에 대해 `페이크 클래스`를 만들어야 한다.

## 느낀점

- 이번 섹션을 읽으면서 페이크 객체라는 걸 처음 알게 됐다. 미션하면서 가능하면 한 번 쯤 사용해봐야겠다.
- 어제 검프가 말한 대로 프로덕션 코드에는 영향을 미치지 않으니까 인터페이스 내에 페이크 클래스를 작성하는 건 괜찮은 방법인 것 같다.