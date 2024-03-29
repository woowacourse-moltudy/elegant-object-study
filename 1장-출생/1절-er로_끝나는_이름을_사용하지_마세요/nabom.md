## 정리

클래스란? 객체의 팩토리

객체는 연결장치가 아니라 대표자여야 한다. (스스로 결정을 내리고 행동할 수 있는 자립적인 엔티티)

클래스에 이름을 붙일 때는 무엇을 하는지가 아니라 무엇인지를 생각해야 한다.

-er로 끝나는 이름을 사용할 경우 결국 클래스가 무엇을 하는지에 포커싱이 된다.

## 느낀점

첫 장부터 객체지향의 중요 요소인 '객체를 자립적인 엔티티로 존중한다'라는 생각이 잘 드러나있다.

이 장의 핵심인 '무엇을 하는지' 가 아니라 '무엇인지'를 생각해야 한다라는 말이 있지만 이 점은 백프로 찬성하기는 힘들다. 물론, '객체지향' 만을 바라봤을 경우 객체가 '무엇'인지를 포커싱하는 것이 옳지만 '객체지향'의 한계로 인해 'AOP(관점지향)'가 나와 '무엇을 하는지'에 대한 포커싱도 생겨났다.

이 책에서 '-er'로 끝나는 잘못된 이름을 가진 클래스의 예시를 보여준다. 'Manager', 'Controller', 'Validator' 등등. 대부분의 예시는 스프링에서 내부적으로 'AOP'를 사용하는 클래스이다. 즉, 태생적으로 어쩔 수 없이 '무엇을 하는지'에 포커싱이 될 수 밖에 없는 클래스인 것이다. (예시가 잘못되었다고 생각한다.)

우테코에서 프로그램을 짤 때 `Domain` 혹은 `Model` 패키지 내부는 객체지향적으로 짜게 된다. 이때는 '무엇인지'에 포커싱이 되는 것이 맞다고 생각하지만 이 도메인을 뷰와 연결해주거나 (컨트롤러)  뷰에 뿌릴(뷰) 때는 '무엇을 하는지'에 포커싱이 되어야 하는 것이 맞다고 생각한다! 즉, 도메인 혹은 모델 부분이 아니라면 -er로 끝나는 이름을 사용해도 괜찮지 않을까 생각이 든다!
