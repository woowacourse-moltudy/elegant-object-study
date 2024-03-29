# 2.3 항상 인터페이스를 사용하세요

객체는 살아있는 유기체이다.<br>
객체는 다른 유기체들과 서로 소통 하면서 그들의 작업을 지원하고 도움을 받는다.<br>
즉, 객체들이 서로 필요로 하기 때문에 결합(coupled)되는 것이다.<br>
하지만 애플리케이션이 커지기 시작하면서 객체 사이의 강한 결합도(tight coupling)이 생기고, 이는 유지 보수에 영향을 미친다.<br>

<br>

따라서 최대한 객체를 분리(decouple)해야한다.<br>
객체 분리란 상호작용하는 다른 객체를 수정하지 않고도 해당 객체를 수정할 수 있도록 만든다는 것이다.<br>
그리고 이를 위해서 필요한 것이 '인터페이스(interface)'이다.<br>

<br>

강한 결합을 막기 위해 클래스 안의 모든 퍼블릭 메서드가 인터페이스를 구현하도록 만들어야한다.<br>
철학적 관점에서 클래스 존재 이유는 누군가 클래스의 서비스를 필요로 하기 때문인데, 서비스는 계약이자 인터페이스이기에 이것은 어딘가에 문서화되어있어야한다.<br>
즉, 동일한 인터페이스를 구현하는 여러 클래스들이 존재하고 언제든 대체 가능하게 만들어야한다. (느슨한 결합도, loose coupling)<br>

<br>

# 느낀점

여러 미션을 진행하면서 인터페이스를 통해 결합도를 낮췄을 때의 이점을 체감했다.<br>
인터페이스를 잘 활용하면 여러 형식의 패턴으로 유연하게 코드를 작성할 수 있었다.<br>
