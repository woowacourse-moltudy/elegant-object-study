# 2.5 퍼블릭 상수(Public Constant)를 사용하지 마세요

## 정리
```
public class Constants {
    public static final String EOL = "\r\n";
}
```
- 해당 클래스는 가시성이 public이기 때문에 클래스 로더에 의해 로딩된 모든 클래스들이 상수에 접근할 수 있다.
    - 이는 클래스의 결합도(coupling)을 높이고, 응집도(cohesion)을 낮춘다. 👉 좋지 않은 설계이다.
<br/>

```
class EOLString {
    private final String origin;
    
    EOLString(String src) {
        this.origin = src;
    }

    @Override
    String toString() {
        return String.format("%s\r\n", origin);
    }
}
```
- 객체는 데이터가 아니라 <b>기능</b>을 공유해야 한다.
- 따라서, 기능을 공통으로 제공할 <b>새로운 클래스</b>를 추가한다.
<br/>

- Constants 클래스에 결합되는 것과 EOLString 클래스에 결합되는 것 사이에는 큰 차이가 없어 보인다.
- 그러나, EOLString에 대한 결합은 <b>계약(contract)</b>를 통해 추가됐다.
    - 계약에 의한 결합은 분리가 가능하기 때문에 유지보수성을 저하시키지 않는다.
    - 즉, EOLString은 계약에 따라 행동하며 클래스 내부에 계약의 의미를 캡슐화한다.
<br/>

- 아무리 사소해 보이는 상수라도 항상 작은 클래스를 이용해서 대체해야 한다.
- Java의 열거형(enum)에 대해서도 동일한 규칙이 적용된다.

## 느낀점

- 그동안은 중복되는 상수를 각 클래스 안에 `private static final`로 여러 번 선언해서 사용했다.
    - 이번 주제를 읽고 중복되는 상수는 작은 클래스로 분리해서 활용하는 게 좋을 것 같다는 생각이 들었다.
- 그런데, 굳이 enum도 작은 클래스 여러 개로 분리하는 게 맞는 방법일지는 모르겠다.
    - 오히려 클래스 수만 많아지고 복잡해질 것 같다.