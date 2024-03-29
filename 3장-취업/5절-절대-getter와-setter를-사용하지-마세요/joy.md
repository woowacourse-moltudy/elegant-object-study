# 절대 getter와 setter를 사용하지 마세요
## 정리
getter, setter는 객체를 단순한 자료구조로 만든다.
자료구조의 데이터는 수동적인 존재였다. 하지만 OOP에서 데이터는 객체안에 캡슐화되었고 능동적인 존재가 되었다.
유지보수성을 높이려면, 가시성의 범위를 축소해서 사물을 단순화시켜야한다. 이해해야하는 범위가 작을수록, 유지보수성이 향상되고 수정하기 쉬워진다.
get/set 접두사는 객체의 데이터를 직접 노출시키는 것과 다름없다. 

## 느낀점
getter/setter를 사용하지 말라는 의견에 100% 동의한다!
getter/setter에 관한 챕터였지만 절차지향과 객체지향의 차이에 대해 더 많이 배운것 같다.
이번장에서 말하는 `코드`는 객체(혹은 자료구조)를 다루는 외부의 코드를 의미하는 것 같다.
