# 1.2 생성자 하나를 주 생성자로 만드세요

## 정리
- Java는 메소드 오버로딩(method overloading)을 지원해서 여러 생성자를 만들 수 있다.
- 클래스의 응집도(cohesion)가 높고, 클래스가 견고할수록 적은 수의 메소드와 많은 수의 생성자가 존재한다.
  - 한 클래스에는 2-3개의 메소드와 5-10개의 생성자를 포함하는 게 적당하다.
  - 단일 책임 원칙(single responsibility principle)을 지킬 가능성도 높아진다.
- 클래스에는 한 개의 주(primary) 생성자와 여러 개의 부(secondary) 생성자를 만드는 게 좋다.
  - 클래스의 유연성을 높일 수 있다.
  - 코드의 복잡성을 줄이고 중복을 제거할 수 있다.
```
class Cash {
  private int dollars;
  
  Cash(float dlr) {
    this((int) dlr);
  }
  
  Cash(String dlr) {
    this(Cash.parse(dlr));
  }
  
  Cash(int dlr) {
    this.dollars = dlr;
  }
}
```
- 결국, 핵심은 <b>유지보수성</b>이다.

## 느낀점
- 그동안 미션을 하면서 한 개의 주 생성자와 여러 개의 부 생성자를 만드는 것에 대한 이점을 얻을 수 있었다.
  - 확실히 코드가 간결해지고 중복을 줄일 수 있었다.
- 그래서 이 내용은 전반적으로 동의한다.
- 그렇지만, 한 클래스에는 2-3개의 메소드와 5-10개의 생성자를 포함하는 게 적당하다는 부분은 아직 잘 모르겠다.
  - 해당 문장 바로 뒤의 '이 값을 뒷받침할 만한 과학적인 근거는 없으며, 임의로 정했을 뿐입니다.' 문장 때문에 설득당하지 못한 것 같다.
