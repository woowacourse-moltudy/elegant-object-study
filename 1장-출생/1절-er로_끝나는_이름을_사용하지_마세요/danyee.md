# 1.1 -er로 끝나는 이름을 사용하지 마세요

## 정리
- 클래스는 객체의 팩토리(factory)이다.
- 클래스는 객체를 인스턴스화(instantiate)한다.
- 클래스는 필요할 때 객체를 꺼낼 수 있고, 더 이상 필요하지 않은 객체를 반환할 수 있는 객체의 웨어하우스(warehouse) 같은 존재이다.
- 팩토리 패턴 ≒ new 연산자
```
Class Shapes {
  public Shape make(String name) {
    if (name.equals("circle") {
      return new Circle();
    }
    if (name.equals("rectangle") {
      return new Rectangle();
    }
    throw new IllegalArgumentException("not found");
  }
}
```
- 클래스의 이름은 <b>클래스가 무엇인지(what he is)</b>에 기반해서 지어야 한다. 무엇을 하는지(what he does)에 기반하면 안 된다.
  - ex. Cash, USDCash, CashInUSD (O)
  - ex. CashFormatter (X)
- 객체는 그의 역량(capability)으로 특정지어져야 한다.
- 객체는 캡슐화된 데이터의 대표자(representative)이다. 연결장치(connector)가 아니다.
- 내가 누구인지 ≠ 내가 무엇을 하는지
  - ex. 리스트(내가 누구인지)는 인덱스 번호를 통해 특정 위치의 요소를 선택할 수 있다(내가 무엇을 하는지).
  - ex. SQL 레코드(내가 누구인지)는 임의의 셀에 저장된 정수값을 조회할 수 있다(내가 무엇을 하는지).

## 느낀점
- 하나의 언어에 국한되지 않고 다양한 언어로 예시를 보여줘서 코드를 읽는 시각을 조금이나마 넓힐 수 있었다.
- 책의 저자는 클래스 이름을 <b>-er</b>, <b>-or</b>로 끝내지 말라고 주장하며, Controller도 네이밍이 잘못됐다고 말한다. 근데, Controller처럼 관례로 사용되는 네이밍도 굳이 피해야 하나? 의문점이 든다.
