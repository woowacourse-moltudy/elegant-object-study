# 1. -er로 끝나는 이름을 사용하지 마세요.

클래스는 객체의 능동적인 관리자이다. (클래스는 객체의 어머니이다.)

클래스 이름을 짓는 적절한 방법은 객체가 노출하고 있는 기능에 기반한 것이 아닌, 클래스가 무엇인지에 기반해야한다.
예를 들어, CashFormatter가 아닌 Cash라고 명명해야한다.
즉, 객체는 그의 `capability`로 특징지어져야한다.

여기서 -er로 끝나는 이름을 짓는다면, 그것은 바로 **기능에 기반하여 클래스를 명명했다**고 볼 수 있다.
ex. Manager, Controller, Handler, Converter
이와 상반된 명명으로는 Target, Content, EncodedText 등이 있다.

## 내 의견
기능에 기반하여 클래스명을 자주 짓는다. Controller를 제외한다 하더라도 PointCalculator, ResultMapper등 클래스가 하는 기능에 초점을 맞춰 클래스명을 짓는 것 같다. 
이렇게 짓는 이유는 클래스를 생성할 때 무엇인지에 기반한 것이 아니라 기능에 기반했기 때문이다. (이것부터가 잘못된 것인가..? 예고르 형님,,)
예를 들어, 포인트를 계산해주는 기능을 담당하는 클래스를 만들자! 라는 생각으로 PointCalculator를 만들고, PointCalculator 내부에는 포인트를 계산해주는 기능이 주로 담긴다. 
만약 PointCalculator를 단순히 CalculatedPoint / Point 등으로 명명한다면 왠지 도메인인 것 같은 느낌이 들고... 그 객체의 기능이 모호하게 느껴진다.
이러한 클래스의 경우에도 CalculatedPoint / Point와 같이 명명하는 것이 맞을까?
