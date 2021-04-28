# 2.8 모의 객체(mock) 대신 페이크 객체를 사용한다.

테스트를 최적화하기 위한 도구, 모킹(mocking)<br>


```java
Exchange exchange = Mockito.mock(Exchange.class);
Mockito.doReturn(1.15)
	.when(exchange)
    .rate("USD", "EUR");
Cash dollar = new Cash(exchange, 500);
Cash euro = dollar.in("EUR");
assert "5.75".equals(euro.toString());
````

모킹은 다음과 같이 사용한다.<br>
하지만 예고르씨는 모킹 대신 '페이크 객체(Fake Obejct)'를 사용할 것을 권한다.<br>

```java
interface Exchange {
    float rate(String origin, String target);
    final class Fake implements Exchange {
    	@Override
        float rate(String origin, String target) {
        	return 1.2345;
        }
    }
}

Exchangeb exchange = new Exchange.Fake();
Cash dollar = new Cash(exchange, 500);
Cash euro = dollar.in("EUR");
assert "6.17".equals(euro.toString());
```

페이크 클래스를 사용하게 되면 테스트를 더 짧게 만들 수 있기 때문에 유지 보수성이 향상된다.<br>
반면 모킹은 테스트 코드가 길어지고 이해하기 어려워 리팩토링에 어려움이 생길 수 있습니다.<br>

모킹을 사용해 본적이 없어서 제대로 이해했는 지 모르겠지만,<br>
예고르씨 말대로 페이크 클래스 내부에서 테스트코드를 작성해준다고 가정해보았을 때 테스트 코드가 많아질 수록 내부 클래스 코드가 길어질 텐데 그런 부분도 고려하고 저렇게 하는 것이 좋다고 판단한걸까 🤔<br>