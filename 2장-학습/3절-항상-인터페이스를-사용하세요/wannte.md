# 2.3 항상 인터페이스를 사용하세요

## 내용 정리
객체 사이의 강한 결합도가 심각한 문제가 됨. 유지보수성을 높이기 가장 휼륭한 방법이 인터페이스!
인터페이스에 정의되지 않은 public 메소드를 가지고 있으면 안된다. 이는 당연하게도 다른 클래스로 하여금 강하게 결합하게 만든다.

서비스는 계약이자 인터페이스고, 문서화되어있어야한다.(인터페이스의 방식으로)
서비스의 제공자들(클래스)들이 서로 경쟁한다.

쉽게 서로를 대체할 수 있어야하므로, 느슨한 결합을 가지게 된다.

## 느낀점
인터페이스로 기능을 따로 정의해야한다고 들었던 기억이 있고, 이 글이 그 근거를 잘 설명해주고 있다.

`하지만, 실제 구현에서는 어느 시점에서 인터페이스의 분리를 진행해 나가야할까?`

처음 구현을 진행하여 구성도를 그릴 때 부터, 필요한 기능들을 다 작성 문서화해두고, interface부터 만들기를 시작해야할 것인가?
아니면, 우선 돌아가게끔만 작성을 하고, 추가적으로 대체 가능성이 확인되었을 때, 이를 인터페이스로 분리하는 것이 좋을까?

그리고 모든 기능을 인터페이스로 다 분리하는 것이 좋은 구현일까?
