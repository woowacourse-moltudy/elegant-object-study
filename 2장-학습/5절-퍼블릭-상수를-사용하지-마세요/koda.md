# 2.5 퍼블릭 상수(Public Constant)를 사용하지 마세요

## 내용

코드의 중복을 줄이기 위해서 public constant를 자주 사용하는데 관련하여 두가지 문제가 발생하기 때문에 사용을 지양해야 한다.

1. 결합도 증가

   - 중복을 줄이기 위해 어느 한곳에 선언된 퍼블릭 함수를 다른 클래스 여기저기서 공용으로 사용하게 된다면 그 다른 클래스들은 퍼블릭 상수가 선언된 객체와 결합되어 의존하는 것이다.

2. 응집도 감소

   - 객체가 스스로 문제를 해결하는 것이 아니라 외부에 의존하여 문제를 해결하면 응집도가 감소된다.

   - 상수는 의미없이 그냥 하드코딩된 어떠한 데이터 덩어리일 뿐이다. 그렇기 때문에 이러한 데이터를 공유하는 것이 아니라 기능을 하는 능동적인 객체로 **기능을 공유**해야 한다.

     ```sql
     //한 줄을 추가하는 기능을 공유하고 싶을 경우 퍼블릭 함수로 /r/n을 추가하지 마라
     class EOLString {
     	private final String origin;
     	EOLString(String src) {
     		this.origin = src;
     	}
     	
     	@Override
     	String toString() {
     		return String.format("%s\\r\\n", origin)
     	}
     }
     ```

즉, 퍼블릭 상수가 의미하는 계약을 준수하는 **새로운 클래스**를 만드는 것이 적절하다.

## 의견

- 작가가 예시로 든 방식으로 구현하는 것을 처음 봐서 굉장히 신선했다. 그리고 퍼블릭 상수가 어떠한 의미나 계약을 준수하는 무엇인가로 생각하기보다 작가가 말했던 것처럼 반복되는 것을 줄이고자 하는 하드코딩 덩어리처럼 내 스스로도 여겼다는걸 알게 되었다.
- 꽤 재미있는 방식의 구현이어서 다음에 다른 것을 구현할 때 한번 적용해보고 싶다.
- 객체지향이라는 것은 모든 것을 계약을 준수하는 능동적인 객체의 집합으로 보고 상호 협력하도록 하는 것이라는 것을 다시한번 알게 된 것 같다.