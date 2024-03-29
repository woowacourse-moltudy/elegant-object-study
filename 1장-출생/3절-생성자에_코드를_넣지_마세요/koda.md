# 1.3 생성자에 코드를 넣지 마세요

## 내용

앞서 하나의 주 생성자와 여러 부생성자를 만들어서 객체가 유연하게 활용될 수 있도록 하라는 챕터가 있었다. 이번 챕터는 그 주생성자에 아무 코드를 넣지 말라는 취지의 글이다. 그 이유는 다음으로 요약할 수 있다. 

> 가벼운 ctor은 설정하기 쉽고 투명하게 사용할 수 있기 때문에 객체를 더 빠르게 만들 수 있다는 점이 바로 그것입니다.

주 생성자에 코드를 넣지 말고 오직 `인스턴스화` 하는 작업만 하자! 이후에 파싱이 필요한 작업의 경우는 lazy 하게 처리하는 것이 좋다. 

- 직접 제어하며 파싱을 하므로 최적화가 가능하다.

## 의견

- 필자가 말한대로 주 생성자에 코드를 넣지 않고 파싱의 경우 이후 필요한 시점에서 파싱을 하는 것이 주도적으로 최적화가 가능하다는 점에서 좋다고 생각한다. 이런 식의 코드 흐름은 한번도 생각해 본 적이 없는데 이번에 처음 이런 코드를 보면서 생각이 트인 것 같다.

## 의문

- 그럼 검증 메소드 같은 경우는 어디서 수행하면 좋을까? 검증 메소드는 외부에서? 그렇지만 일급컬렉션의 이점 중 하나는 스스로 검증을 하면서 값을 보장할 수 있는 것이라고 생각하는데 생성자에서 하지 않으면 어디서 해야 할까?