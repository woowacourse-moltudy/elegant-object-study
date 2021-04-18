# 1.3 -생성자에 코드를 넣지 마세요

## **정리**

### **생성자에는 코드가 없어야(Code-Free)하고, 오직 할당문만 포함해야해요**

```java
class StringAsInteger implements Number {
    private String text;

    public StringAsInteger(String text) {
        this.text = text;
    }

    public int intValue() {
        return Integer.parseInt(this.text);   
    }
}
```

생성자에 코드가 없는 모습을 볼 수 있어요. intValue()를 호출 할 때 마다 파싱을 하니, 느린 것이 아닌가? 라는 의문점이 들 수 있어요.

```java
class StringAsInteger implements Number {
    private int number;

    public StringAsInteger(String text) {
        this.number = Integer.parseInt(text);
    }

    public int intValue() {
        return this.number;
    }
}
```

위와 같은 코드는 텍스트 파싱은 객체를 초기화 하는 시점에 단 한번 수행하기 때문에 효율적으로 보이지만, 최적화가 불가능해요. 만들때 마다 파싱이 수행되기 때문에 실행 여부를 제어할 수 없기 때문이죠.

### **인자를 전달된 상태 그대로 캡슐화하고 나중에 요청이 있을 때 파싱하도록 하면, 파싱 시점을 자유롭게 결정할 수 있어요.**

파싱이 여러 번 수행되지 않도록 하고 싶다면 **데코레이터를(decorator)**를 추가해서 최초의 파싱을 캐싱할 수 있어요.

```java
class CahcedNumber implements Number {
    private Number origin;
    private List<Integer> cached = new ArrayList<>();

    public CahcedNumber(Number number) {
        this.origin = number;
    }

    public int intValue() {
        if (this.cached.isEmpty()) {
            this.cached.add(this.origin.intValue());
        }
        return this.cached.get(0);
    }
}
```

```java
Number number = new CachedNumber(new StringAsInteger("123"));

number.intValue();    //첫 번째 파식
number.intValue();    // 여기에서는 파싱하지 않음 
```

객체를 인스턴스화하는 동안 객체를 만드는 일 이외에는 어떤 일도 수행하지 않아요. 

생성자에 코드를 없에면 사용자가 쉽게 제어할 수 있는 투명한 객체를 만들 수 있으며, 객체를 이해하고 재사용하기도 쉬워져요.

## **의견**

생성자에 코드를 없애다 보면, 클래스가 많아지게 돼요. 클래스를 많이 만드는게 서비스에 좋을 듯 한거 같기도 하고, 아닌거 같기도 하고, 더 많은 코드를 짜봐야 알겠어요.