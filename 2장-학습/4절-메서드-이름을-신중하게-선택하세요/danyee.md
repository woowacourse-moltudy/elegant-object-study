# 2.4 메서드 이름을 신중하게 선택하세요

## 정리
- 빌더(builder)
    - 이름을 <b>명사</b>로 짓는다.
    - 반환타입은 절대 void가 될 수 없다. 항상 무언가를 반환한다.
    - ex. float speed();
    - ex. String parsedCell(int x, int y);
- 조정자(manipulator)
    - 이름을 <b>동사</b>로 짓는다.
    - 반환타입은 항상 void이다.
    - ex. void save(String content);
    - ex. quicklyPrint(int id);
- 예외: Boolean 값을 결과로 반환하는 경우
    - 이름을 <b>형용사</b>로 짓는다.
    - 반환타입은 항상 boolean이다.
    - ex. boolean empty();
    - ex. boolean readable();

## 느낀점

- 메소드 이름을 이런 기준으로 선택할 수 있구나 생각할 수 있었던 주제였다.
- 그래도 클린 코드 원칙에 따라 메소드 이름은 동사로 지을 생각이다.