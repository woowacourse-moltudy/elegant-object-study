
# **2.5 -퍼블릭 상수(Public Constant)를 사용하지 마세요**

## **정리**

### 상수를 이용한 공유 메커니즘은 캡슐화와 객체지향적인 사고 전체를 부정하는 일이에요

아래 예제는 잘 사용된 예제에요 

```java
class Records {
    private static final String EOL = "\r\n";

    void write(Writer out) {
        for (Record rec : this.all){
            out.write(rec.toString());
            out.write(Records.EOL);;
        }
    }
}
```

필요할때 마다 반복적으로 EOL을 사용하고 싶지 않기에. 객체 내부에서만 사용되는 EOL은 잘 사용되고 있어요.

하지만 아래와 같이 새로운 객체가 생성됐다고 가정해보면,

```java
class Rows {
    private static final String EOL = "\r\n";

    void write(PrintStream pnt) {
        for (Row row : this.all){
            pnt.print(
                    "{ $s }%s", row, Rows.EOL
            )
        }
    }
}
```

처음 작성했던 객체와 위의 객체는 공통점이 전혀 없어요. 하지만 EOL이라는 private 상수를 정의하고 있어요. 

이때 중복을 제거해야해요. 

### 중복을 제거하는 방법?

```java
public class Constants {
    public static final String EOL = "\r\n";
}
```

중복 제거를위해 위와 같이 선언했어요. 

```java
class Records {
    void write(Writer out) {
        for (Record rec : this.all){
            out.write(rec.toString());
            out.write(Constants.EOL);;
        }
    }
}

class Rows {
    void write(PrintStream pnt) {
        for (Row row : this.all){
            pnt.print(
                    "{ $s }%s", row, Constants.EOL
            )
        }
    }
}
```

중복 문제를 '해결'한 것 처럼 보이지만, 중복을 피하려다 더 큰 문제를 추가해버리는 꼴이 됐어요.

첫 번째 문제는 **결합도(coupling)**가 높아 진 것이고, 두 번째 문제는 **응집도(cohesion)**가 낮아진 것이에요.

### 상수는 멍청해요

자신의 존재 이유를 알지 못하는 텍스트 덩어리에 불과해요. 즉, 어디에서도 쓰이는 상수는 삶의 의미가 명확하지 않아요.

### 객체 사이에 데이터를 중복해서는 안돼요, 대신 기능을 공유할 수 있도록 새로운 클래스를 만들어야 해요

```java
class EOLString {
    private final String origin;

    EOLString(String src) {
        this.origin = src;
    }

    @Override
    public String toString() {
        return String.format("%s\r\n", origin);
    }
}
```

계약에 의해 결합되었고, 계약에 의한 결합은 언제든지 분리가 가능하기에 유지보수성을 저하시키지 않아요.

EOL은 계약에 따라 행동하며 내부에 계약의 의미를 캡슐화 해요.

EOLString이 변경되어야 한다고 하더라도 객체들과 계약(인터페이스)은 동일하게 유지하면서 동작은 변경할 수 있어요.

```java
class EOLString {
    private final String origin;

    EOLString(String src) {
        this.origin = src;
    }

    @Override
    public String toString() {
        if (/* 맥북이면 */) {
            throw new IllegalStateException("맥에선 실행불가!");
        }
        return String.format("%s\r\n", origin);
    }
}
```

### **퍼블릭 상수마다 계약의 의미를 캡슐화하는 새로운 클래스를 만들어야 하나요?**

맞아요

### 수 백개의 단순한 상수 문자열 리터럴 대신 수백 개의 마이크로 클래스를 만들어야 하나요?

맞아요.

```java
String body = new HttpRequest()
                .method("POST")
                .fetch();
```

위의 코드는 아래로 변경할 수 있어요.

```java
String body = new HttpRequest()
                .method(HTTPMethods.POST)
                .fetch();
```

이정도도 깔끔하지만, OOP정신에 어긋나요.

리터럴을 사용하는 대신, 아래와 같이 HTTP 메서드를 표현하는 단순한 클래스를 많이 만드는게 좋아요

```java
String body = new PostRequest(new HttpRequest())
                .fetch();
```

### 열거형(Enum) 클래스도 사용하지 말아요.

## **의견**

이번 절에는 꽤나 단정적인 문장들이 많아요. 어떠한 지식을 이렇게 강제로 주입받는 것은 처음이네요. 

OOP란 무엇일까에 대해 항상 고민했는데, 이러한 부분들부터 OOP적으로 만드는게 진정한 객체지향이 아닐까 생각이 들긴해요. 

클래스들이 많아지는건 정말.. 어렵지만 이해해보려 해요.