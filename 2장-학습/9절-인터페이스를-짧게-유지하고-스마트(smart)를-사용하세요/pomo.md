# 2.9 인터페이스를 짧게 사용하고, smart를 사용하라.

예고르씨는 앞에서부터 계속 클래스를 작게 만들라고 했다.<br>
그의 주장에 따르면 다수의 인터페이스를 구현한 클래스는 메서드가 많아질 수 있기 때문에 인터페이스 또한 작게 유지하라는 것이다.<br>

```java
interface Exchange {
    float rate(String target);
    float rate(String source, String target);
}
```

인터페이스는 구현 클래스가 준수해야할 계약인데, 위와 같은 인터페이스는 구현자에게 많은 것을 요구한다.<br>
즉, source 값이 디폴트로 구현되는 rate(String target)은 포함되어서는 안된다는 것이다.<br>
여기서 예고르는 smart를 사용하라고 말한다.<br>

```java
interface Exchange {
    float rate(String source, String target);
    final class Smart {
        private fianl Exchange origin;
        
        public float toUsd(String source) {
        	return this.origin.rate(source, "USD");
        }
        
        public float eurToUsd() {
        	return this.toUsd("EUR");
        }
    }
 }
 
 
 float rate = new Exchange.Smart(new NYSE()).eurToUsd();
```

솔직히 이렇게 써서 얻는 이점을 크게 못 느끼겠다.<br>
그리고 가독성이 떨어진다. 일단 당장의 예시 코드만 봐도 바로 이해하기에는 어렵다고 느꼈다.<br>

<br>

그리고 개인적인 인터페이스의 이점 중 하나는 구현된 코드를 숨기고 행동 규약만 보여준다는 점이었는데,<br>
이렇게 되면 인터페이스를 통해 공통 코드가 그대로 노출되면서 인터페이스의 이점이 사라진다고 생각했다.<br>

<br>

이뿐만이 아니라 사용하고 싶은 공통 기능에 따라 추상 클래스를 만들고 입맛에 맞게 하위 클래스가 상속받을 수 있을 텐데,<br>
저렇게 인터페이스 내부에서 지정해버리면 하위의 구현 클래스들 모두 영향을 미칠 수 있겠다는 생각이 든다.<br>

<br>

지금 내 생각으로는 이럴거면 쓰지 말라고 하지, 왜 짧게 사용하라는 건지 의문이다.<br>
인터페이스가 어떤 이점을 가지고 사용되는 지 다시 생각해보면서 고민해봐야겠다.<br>