# 2.3 항상 인터페이스를 사용하세요

- 객체들은 서로를 필요로 하기 때문에 결합된다. (협력)
  - 객체지향 세계가 커지면 커질 수록 강한 결합도 문제 발생
- 결합 된 다른 객체를 수정하지 않고도 해당 객체를 수정 할 수 있어야 한다.

## 인터페이스 라는 도구

```java
interface Cash {
	Cash multiply(float factor)
}
```

- Cash는 인터페이스
- Cash는 다른 객체와 의사소통 하기 위해 따라야 하는 계약

```java
class Employee {
	private Cash salary
}
```



- Employee는 Cash의 multiply에 관심이 없다.
- 느슨한 결합도
  - 결합은 되어있지만 구현이 대체 될 수 있다.



# 느낀점 의문점

- public 메소드를 가진 모든 클래스에 대해서 인터페이스를 만들어야 하는가
- 존재하는 여러 타입(클래스)로 부터 추상화를 진행해야하는가 (인터페이스)
- 아니면 추상화를 먼저(인터페이스) 해야 하는가.
- 예전에 검프랑 추상화에 대해서 말을 했던 것
  - 사람들이 살아오면서 무언가를 두드리는 도구들을 추상화 하여 망치가 됨
- 인터페이스를 먼저 정의 하기보다는 구현을 해보면서 추상화를 해야 겠다는 생각이 들 때 추상화를 진행해야 되지 않을까?