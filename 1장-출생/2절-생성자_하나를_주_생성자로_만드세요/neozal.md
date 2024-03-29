# 1-2. 생성자 하나를 주 생성자로 만드세요

### 2 ~ 3개의 메서드와 5 ~ 10개의 constructor 를 가진 객체를 만들어라
- 여기서 말하는 메서드는 public 메서드이다. private 메서드는 예외이다.

### 주 constructor 와 부 constructor 로 나누어서 호출하라. (하나의 주 생성자여 여러개의 부 생성자를 가져라)
```java
class Cash {
    private int dollars;
    
    Cash(float dlr) {
        this((int) dlr);
    }

    Cash(String dlr) {
        this(Cash.parse(dlr));
    }

    Cash(int dlr) {
        this.dollars;
    }
} 
```

- 위 코드에서 주 생성자는 `Cash(int dlr)` 시그니처를 가진 생성자이며, 부 생성자는 나머지 생성자들이다.
주 constructor 모든 부 constructor 뒤에 위치시킨다. -> 유지보수성을 위함

- 이와 같은 코드를 작성하면, 인자의 검증과 같은 로직의 중복을 막을 수 있다(주 생성자에서 한번만 검증하면 된다.).
- 메서드 오버로딩을 이용하면 content(File), contentInCharset(File, Charset)대신 content(File), content(File, Charset)으로 소스를 간결하게 변경 가능.

## 나의 생각
몇가지 생각을 제외하고는 완벽하게 동의한다.

- 2~3개의 메서드와 5~10개의 constructor 를 가진 객체를 만들어라
    - 아주 좋은 practice라고 생각한다. 메서드의 크기를 작게 만든다는 것은, 객체가 처리할 수 있는 데이터(필드)가 작아진다는 이야기가 되며, 이는 응집도를 자연스럽게 올릴 수 있는 방법이 된다.
    
- 주 controller 와 부 controller 로 나누어서 호출하라
    - 저자는 주 controller를 모든 부 controller 뒤에 위치시킨다. 이는 유지보수성과 관련이 있다고 말한다. 하지만 나의 생각은 좀 다르다.
    유지보수성을 위해서라면 주 생성자가 가장 위에 있어야 한다고 생각한다. 저자의 생각은 잘 알 것 같다. 클린코드의 원칙에서 메서드는 "읽는 순서대로" 정의되어야 한다고 한다.
    하지만 생성자는 다르게 생각해야 한다고 생각한다. 생성자는 객체가 생성되는 부분이며, 소스의 중복을 위해 모든 생성과 관련된 로직이 주 생성자에 몰려있을 가능성이 높다.
    따라서 클래스를 처음 봤을때 "생성자"가 가장 처음에 보이는게 맞다고 생각하며 이 편이 유지보수성에 더 도움이 된다고 생각한다.
    
    - 저자는 메서드 오버로딩을 이용하면 간결한 표현이 가능하다고 말하였다. 하지만 이게 과연 맞을까? 일단 클린코드의 원칙에 따라서, 메서드의 인자는 2~3개를 넘지 않는것이 좋다.
    이 가정이 지켜진다고 생각하면, 나는 메서드 오버로딩을 통해서 파라메터를 숨기는 것 보다 메서드의 이름을 통해서 파라메터와 의미를 드러내는편이 더 좋다고 생각한다.
    이 내용은 클린코드에도 있다. 실제로, 클린코드를 읽고 오버로딩 보다는 메서드 이름에 모든덜 드러낸 코드를 작성했을 때, 가독성면에서 더 좋은 느낌을 얻었었다. 
     


