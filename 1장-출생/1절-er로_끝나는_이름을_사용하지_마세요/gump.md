# 1.1 -er로 끝나는 이름을 사용하지 마세요

## **정리**

클래스에 적합한 이름을 짓는 것은 중요해요. 클래스의 이름을 살펴보기 전, 클래스가 무엇인지 알아볼 필요가 있어요.

### **클래스는 동적인 객체의 상태와 행동을 정적인 텍스트로 표현하기 위한 추상화 도구**

말이 조금 어려워요. 좀더 쉽게 얘기하면, 클래스는 `객체의 어머니`라 볼 수 있어요. 

즉, 필요할 때 생성되고, 더이상 필요하지 않은 객체는 반환하는 (어머니와 아이를 생각하면 조금 잔인할 수 있지만) 객체의 창고라고 말할 수 있어요.

### **클래스의 이름을 붙일 땐 `무엇을 하는지(what he does)`가 아닌 `무엇인지(what he is)`를 생각해요**

 여기 숫자를 문자열로 포맷팅을하는 클래스가 있어요.

```java
class NumberFormatter {
    private int number;

    NumberFormatter(int number) {
        this.number = number;
    }

    public String format() {
        return String.format("%d", this.number);
    }
}
```

숫자를 문자열로 변환하기에, 이 클래스는 더할나위 없이 완벽해 보여요.

하지만 이 클래스는 `무엇을 하는지`를 중점적으로 생각하기에, 연결장치에 불과하며 존중할만한 객체가 아니네요.

```java
class Number {
    private int number;

    Number(int number) {
        this.number = number;
    }

    public String toString() {
        return String.format("%d", this.number);
    }

    public double toDouble() {
        return (double)number;
    }
}
```

존중한말한 객체로 변경했어요.

즉, 객체는 `그의 역량(capability)`로 특정지어져야 해요. 객체는 속성이 아니라 할 수 있는 일로 설명해야 해요.

## **의견**

역량을 생각하면 그가 할 수 있는 일이 따라온다는 관점이 멋저요. 이후 클래스 네이밍에 참고해야할 부분들이 많았어요.