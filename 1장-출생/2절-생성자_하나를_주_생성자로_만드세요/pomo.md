# 1.2 생성자 하나를 주 생성자로 만드세요

예고르씨는 올바른 클래스 설계는 많은 수의 ctor(생성자)와 적은 수의 메서드를 포함한다고 말합니다. (2번 강조 😲)
2 ~ 3개의 메서드와 5 ~ 10개의 ctor을 포함하는 것이 적당하다고 말하는데요, 
응집도가 높고 견고한 클래스에는 적은 수의 메서드와 상대적으로 많은 수의 ctor가 존재한다는 것입니다.

단 하나의 ctor인 주(primary) 생성자와 이 주 생성자를 호출하는 부(secondary) 생성자를 만들어야합니다.
예고르씨는 유지 보수성을 위해 항상 주 생성자를 부 생성자 뒤에 위치시킨다고 하는데요
이는 예전에 만들어놓은 생성자를 하나하나 읽어가며 주 생성자를 찾기 힘들 때 맨 뒤에 위치시켜 유지 보수성을 높인다고 합니다!

### 하나의 주 생성자와 다수의 부 생성자의 핵심
중복 코드를 방지하고 설계를 더 간결하게 만들어 유지 보수성을 향상시킨다!
즉, 인자에 따라 설정이 다른 여러 부생성자가 있다고 가정했을 때 그들이 가지는 공통 검증 로직을 주 생성자에서 처리해줄 수 있습니다!

```java
public Lotto {
	private int number;
    
    public Lotto(int number) {
    	if (number < 0) { 	// 양수가 아닌 로또 숫자에 대한 검증 로직
          throw new InvalidLottoNumberException();
        }
    	this.number = number;
    }
    
    public Lotto(String number) {
    	this(Lotto.parse(number)); // int로 변환
    }
 	
    public Lotto(float number) {
    	this((int)number);
    }
}
```

핵심은 내부 프로퍼티는 오직 한 곳(주생성자)에서만 초기화 해야하고 다른 모든 위치(부 생성자)에서는 단순히 인자를 준비(포맷팅, 파싱, 변환)만 해야합니다.

# 느낀점

-er에서 대해서는 완벽히 이해하기 어려웠다.
예를 들어 LottoNumberGenerator라는 친구가 있다고 했을 때,
여기서 말하는 것처럼 이 친구를 LottoNumber 안에서 make()와 같은 식으로 만든다면?

물론 LottoNumber가 예고르씨가 말한대로 절차적인 로직을 제거할 순 있겠지만, 
LottoNumber에 굉장히 많은 코드들이 들어가게 되서 되려 코드의 복잡성이 증가할 수 있다고 생각했다. 🤔
애매하구만,,,