## 2.2 최소한 뭔가는 캡슐화하세요.
앞선 2.1 에서 가능한 적게 캡슐화하라고 했다. 그렇다면 0개는 어떤가?
객체의 필드는 객체의 상태이자 식별자이다. 어떤 것도 캡슐화하지 않은 클래스의 모든 객체는 동일하다. 프로퍼티가 없는 클래스는 정적 메서드와 유사하다. 이 클래스는 아무런 상태와 식별자도 가지지 않고 오직 행동만을 포함한다. 정적 메서드가 존재하지 않고 인스턴스 생성과 실행을 엄격하게 분리하는 순수한 객체지향에서는 기술적으로 프로퍼티가 없는 클래스를 만들 수 없다.

객체가 '무'와 비슷한 어떤 것이 아니라면 무언가를 캡슐화해야한다. 자기 자신을 식별할 수 있도록 하기 위해 무언가를 캡슐화해야한다. 어떤 것도 캡슐화하지 않는 상태는 객체 자신이 세계 전체가 된다. 오직 하나의 세계만 존재할 수 있기 때문에 이 클래스는 오직 하나만 존재해야한다.

### 의견
아무것도 캡슐화하지 않는다는 것은 객체를 식별할 수 있는 것이 아무것도 없다는 뜻인 것 같다. 객체의 식별자로서 최소 1개 이상의 프로퍼티는 필요하기 때문이다.
하지만 궁금한 점은, 정적 메서드와 같이 프로퍼티가 없는 경우이다. 이 경우 우선 뒷 장(3.2)에서도 절대 정적 메서드를 사용하지 말라고 하긴 하지만, 아직까지 왜!? 사용하면 안되는지가 이해가 잘 안된다. 책 내용에서 `어떤 것도 캡슐화하지 않는 상태는 객체 자신이 세계 전체가 된다. 오직 하나의 세계만 존재할 수 있기 때문에 이 클래스는 오직 하나만 존재해야한다.`라고 이야기했는데, 정적 메서드의 생성자를 private으로 막아두고 static method만 외부에서 사용할 수 있도록 하면 오직 하나만 존재할 수 있도록 하는 것을 만족시킬 수 있는거 아닐까 ?? (잘 모르겠다. ㅠ)

