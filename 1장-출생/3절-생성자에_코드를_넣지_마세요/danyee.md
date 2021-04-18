# 1.3 생성자에 코드를 넣지 마세요

## 정리
- 객체 초기화에는 코드가 없어야(code-free)하고 인자를 건드려서는 안 된다.
- 대신, 필요하다면 인자들을 다른 타입의 객체로 감싸거나 가공하지 않은 형식(raw form)으로 캡슐화해야 한다.
<br/>

- 객체를 초기화하는 시점에 곧장 텍스트를 숫자로 변환하지 말고, 실제로 사용하는 시점까지 객체의 변환 작업을 연기해야 한다.

```
class Cash {
    private Number dollars;

    Cash (String dlr) {
        this.dollars = new StringAsInteger(dlr);
    }
}

class StringAsInteger implements Number {
    private String source;

    StringAsInteger(String src) {
        this.source = src;
    }

    int intValue() {
        return Integer.parseInt(this.source);
    }
}
```
<br/>

- 파싱이 여러 번 수행되지 않도록 하고 싶다면 데코레이터(decorator)를 추가해서 최초의 파싱 결과를 캐싱하면 된다.

```
class CachedNumber implements Number {
    private Number origin;
    private Collection<Integer> cached = new ArrayList<>(1);

    public CachedNumber(Number num) {
        this.origin = num;
    }

    public int intValue() {
        if (this.cached.isEmpty()) {
            this.cached.add(this.origin.intValue());
        }
        return this.cached.get(0);
    }
}
```
<br/>

- 생성자에서 코드를 없애면 사용자가 쉽게 제어할 수 있는 투명한 객체를 만들 수 있다.
- 또한, 객체를 이해하고 사용하기 쉬워진다.
- 결국, 객체는 요청을 받을 때만 행동하고 그 전에는 어떤 일도 하지 않는다. 👉 좋은 방식으로 매우 게으르다(lazy).

## 느낀점

- 해당 내용을 읽으면서 프리코스 때 생성자에 코드를 넣었던 기억이 떠올랐다.
    - 저자가 사용한 예제처럼 `Integer.parseInt()` 사용했던 거 같은데,, 😂
    - 새삼 그때는 코딩 정말 아무것도 모르고 했구나 싶다.
- 생성자에 코드를 넣지 않았을 때의 이점이 생각보다 큰 것 같다.
- 데코레이터로 최초의 파싱 결과를 캐싱할 수 있다는 걸 처음 알았다. 다음에 미션하면서 활용해봐야겠다!