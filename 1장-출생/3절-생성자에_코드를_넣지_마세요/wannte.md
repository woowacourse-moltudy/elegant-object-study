# 1.3 생성자에 코드를 넣지 마세요
## 내용 정리
### Don't touch the argument
```java
class Cash {
  private int dollars;
  Cash(String dlr) {
    this.dollars = Integer.parseInt(dlr);
  }
}
```
-> code-free 해야 함. 다른 타입의 객체로 감싸거나, Raw form 으로 캡슐화해야 함.
### 사용하는 시점까지 객체의 변환 작업을 연기한다.
객체 생성시 parsing vs 사용시 parsing
사용시 parsing 했을 경우 cache를 이용하여 최적화가 가능.

| 객체를 인스턴스화하는 동안에는 객체를 build하는 일 이외에는 어떤 일도 수행하지 않습니다.

## 느낀 점
생성자에서의 유효성 검사에 관해 고민을 했었다. [생성자에서의 유효성 검사에 관하여 블로그 정리](https://velog.io/@wannte/%EA%B0%9D%EC%B2%B4-%EC%83%9D%EC%84%B1%EC%8B%9C-%EC%9C%A0%ED%9A%A8%EC%84%B1-%EA%B2%80%EC%82%AC%EC%97%90-%EA%B4%80%ED%95%98%EC%97%AC)

글을 써가면서, primitive value를 캡슐화시켜 사용하였는데, 이는 단순히 그 책임만을 분리한 것이고, 객체스러운 구현은 아니었다.


> 생각을 정리해보면, 객체를 단순히 저장의 수단 정도로 생각했던 것 같아요. 그 저장의 책임만을 분리해서 이를 객체라 정의하고 사용했던 것 같아요! 객체 내부의 구현을 외부에 숨긴다라는 말에 의문을 가지고 있었어요. 저장된 방식은 정해져 있고, 이를 외부에서 사용하는데 있어서, 숨김으로써 가지는 장점이 무엇이 있을까? 단순히 사용하기 편해서?
이번 단원을 읽으면서, 이 부분에서 가려운 부분을 긁어준 느낌이에요. 생성자의 역할을 줄이고, 내부 구현이 숨겨진 메소드에서 이 부분을 다른 방식으로 정리하여 사용하는 방식으로요.(parseInt를 메소드에서 처리하는 방법)


생성할 때의 인수를 그대로 가지고 있으면서도, 그 메소드의 구현 방식을 수정함으로써 더 객체스럽게 사용할 수 있다.


## ?
```java
class StringAsInteger implements Number {
  private Sting text;
  StringAsInteger(String txt) {
    this.text = txt;
  }
  
  public int intValue() {
    return Integer.parseInt(this.text);
  }
}
```
로또 미션을 기억해보자. 돈을 입력받을 때 양의 정수만을 허용하고자 한다.
그렇다면, 지금의 구현은 객체를 생성한 이후에, validation 과정을 추가적으로 진행하여 검증 과정을 거쳐야 한다.
생성자와 검증 메소드가 강하게 결합하게 되서, 이와 같은 경우에서는 생성장에서 진행한느 것이 바람직 하지 싶다.
