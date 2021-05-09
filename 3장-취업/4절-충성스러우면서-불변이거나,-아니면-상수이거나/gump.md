# **3.4-충성스러우면서 불변이거나, 아니면 상수이거나**

## **정리**

### 세상을 충분히 불변 객체로 모델링 할 수 있어요. 사람들이 혼란스러워 하는 이유는 서로 다른 개념인 `상태(state)`와 `데이터(data)`에 관해 오해하기 때문이에요

예제를 먼저 볼게요

```java
class WebPage {
    private final URI uri;

    WebPage(URI path) {
        this.uri = path;
    }

    public String content() {
        // HTTP GET 요청을 전송해서,
        // 웹 페이지의 컨텐츠를 읽은 후,
        // 읽혀진 컨텐츠를 UTF-8 문자열로 반환 
    }
}
```

이때의 WebPage는 불변일까요 가변일까요?

### 핵심은 객체가 살아있는 동안 상태가 변하지 않는다는 사실이에요

위의 예제에서의 WebPage는 분명히 불변이에요.

이부분이 많은 사람들이 오해하는 부분이에요

### 사람들은 불변 객체의 메서드를 호출할 때마다 상수처럼 매번 동일한 데이터가 반환되리라 기대해요

불변 객체가 생성되고 나면 모든 메서드가 항상 동일한 값을 반환하여, 반환된 결과를 100% 에측할 수 있다는 말은 적절해보이지만, 이런 사고방식은 틀렸어요. 

상수처럼 동작하는 객체는 단지 불변성의 `특별한 경우(corner case)`일 뿐이기 때문이에요.

### 불변객체는 그 이상이에요

비록 content() 메소드 결과를 예측할 수 없더라도 WebPage는 불변 객체에 속해요. WebPage 클래스는 실제 웹 페이지와 통신하기 때문에 우리는 이 객체가 무엇을 돌려줄지 몰라요. 

객체의 행동을 예상할 수는 없지만, 그럼에도 이 객체는 불변이에요. 결과가 변하기 때문에 `상수`는 아니지만, 객체가 대표하는 엔티티에 `'충성하기(loyal)`' 때문에 불변 객체로 분류돼요.

### 객체란 디스크에 있는 파일, 웹 페이지, 바이트 배열, 해시맵, 달력의 월과 같은 실제 엔티티(real-life)의 대표자예요.

여기서 실제라는 것은 가시성 범위(scope of visibility)밖에 존재하는 모든 것을 의미해요. 

아래 코드에서 객체 f는 디스크에 저장되어 있는 파일을 대표해요 

```java
public void echo() {
    File f = new File("/tmp/test.txt");
    System.out.println("File size: %d". file.length());
}
```

여기서 f의 가시성 범위는 echo() 메서드의 '경계'에 대응해요. 예제에서는 디스크에 저장된 파일의 사이즈를 알아내기 위해 객체 f의 length() 메서드와 의사소통하고 있어요.
코드에서 `f는 '/tmp/test.txt'파일의 대표자`예요. 객체 f는 실제 파일의 입장을 대변해요. 우리의 관점에서 객체 f는 echo() 메서드 안에서만큼은 **파일**이에요 

디스크에 저장된 파일을 다루기 위해 객체는 파일의 **좌표(coordinates)**를 알아야해요. 이 좌표를 다른 말로 객체의 **상태(state)**라고 불러요

WebPage 객체의 상태는 페이지 URI예요. WebPage 객체는 HTTP 프로토콜을 이용해 실제 웹 페이지를 읽어들일 때 HTTP 엔드 포인트의 좌표로 이 URI를 사용해요. File 클래스의 상태는 파일 시스템 상에 위치한 파일의 전체 경로예요. 따라서 앞의 예제에서 객체 f의 상태는 /tmp/test.txt예요. 

### 기본적으로, 모든 객체는 식별자(identity), 상태(state), 행동(behavior)를 포함해요

`식별자`는 f를 다른 객체와 구별해요. `상태`는 f가 디스크 상의 파일에 대해 알고 있는 거에요. `행동`은 요청을 수신했을 때 f가 할 수 있는 작업을 나타내요. 

### 불변객체와 가변객체의 중요한 차이는 불변 객체에는 식별자가 존재하지 않으며, 절대로 상태를 변경할 수 없다는 점이에요

동일한 URI를 가진 두 개의 WebPage 인스턴스를 생성하는 경우 두 개중 무엇을 사용하더라도 아무런 차이가 없기 때문에 두 객체는 동일해요. (객체 팩토리를 완벽하게 구현하려면, 동일한 상탤르 캡슐화 하는 중복된 인스턴스는 생성하지 않아야해요)

### 하지만 Java를 포함한 대부분의 OOP 언어에서는 상태가 동일하더라도 서로 다른 객체라고 판단해요

기본적으로 각 객체는 재정의할 수 있는 자신만의 유일한 식별자를 가져요  

WebPage 클래스 객체들이 포함하는 유일한 상태(식별자)는 URI형태의 페이지 좌표뿐이에요. 

반변에 가변 객체는 완전히 다른 방식으로 동작해요. `가변 객체의 상태는 변경이 가능`하기 때문에, 상태에 독립적인 식별자를 별도로 포함해야 해요

### 완전한 객체 지항세계에서는 불변 객체만 존재하기에 equals()와 hashCode()라는 메서드는 필요하지 않아요

두 메서드의 구현은 모든 클래스에 걸쳐 동일해요. 새롭게 구현하거나 재정의할 필요가 없어요.

캡슐화된 상태만으로도 불변 클래스의 모든 객체들을 식별할 수 있기 때문이에요.

### 상수 리스트(constant list)와 불변 리스트(immutable list)

불변 객체의 컬렉션을 구현하려면 이 두가지 쟁점이 있어요.

### 상수 리스트

```java
public class Cards {
    private final List<Card> cards;

    public Cards(final List<Card> cards) {
        this.cards = new ArrayList<>(cards);
    }

    public List<Card> getCards() {
        return Collections.unmodifiableList(cards);
    }

    public Cards add(final Card card) {
        List<Card> cards = new ArrayList<>(this.cards);
        cards.add(card);

        return new Cards(cards);
    }
```

위와 같은 객체는 불변 객체라 부르는 것 보단 `상수 객체`로 부르는 것이 더 좋아요.

cards는 Cards의 상태인 동시에 Cards가 대표하는 엔티티와 동일해요. 객체는 리스트를 대표하며, 이 객체의 상태는 바로 그 리스트예요.

### 불변 리스트

```java
public class Cards {
    private final List<Card> cards;

    public Cards(final Card... cards) {
        this(Arrays.asList(cards));
    }

    public Cards(final List<Card> cards) {
        this.cards = new ArrayList<>(cards);
    }

    public List<Card> getCards() {
        return Collections.unmodifiableList(cards);
    }

    public void add(final Card card) {
        this.cards.add(card);
    }
}
```

add를 한다고 해서 가변이 되는 것이 아니에요. 

객체를 대표하는 상태를 가지고 있고, 이는 변하지 않아요.

(final시 리스트의 요소들의 불변을 보장하는 것이 아닌, 리스트 변수가 가르키고 있는 메모리의 불변을 보장)

즉 위의 객체도 불변이 맞아요.

### 상수 객체가 설계하고, 유지보수하고, 이해하기 더 편하기 때문에 불변 객체보다는 상수 객체를 사용하는 편이 더 좋아요.

2.6에서 불변 객체에 대해 이야기했던 대부분의 내용은 불변 객체의 특별한 경우인 상수 객체와 관련이 있어요.

## **의견**

이전에 나봄과 일급 컬렉션의 불변에 대해 얘기한적이 있는데, 이부분을 더 자세히 볼걸 그랬어요.

같은 불변이지만, 상수라 표현함으로써 불변성이 더 커지는 것을 알게됐어요.