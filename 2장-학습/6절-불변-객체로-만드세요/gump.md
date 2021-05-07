# **2.6 -불변 객체로 만드세요**

## **정리**

### 모든 클래스를 상태 변경이 불가능한 불변 클래스(immutable class)로 구현하면 유지보수성을 크게 향상시킬 수 있어요.

인스턴스를 생성한 후에 상태를 변경할 수 없는 객체를 불변 객체라고 불러요. 

아래와 같은 클래스는 상태 변경이 가능하기 때문에 가변 객체라고 불러요 

```java
class Cash {
    private int dollars;

    public void setDollars(int val) {
        this.dollars = val;
    }
}
```

아래와 같이 변경한다면 상태를 변경할 수 없게 돼요.

```java
class Cash {
    private final int dollars;

    Cash(int val) {
        this.dollars = val;
    }
}
```

인스턴스 변수에 final을 붙이면 변수의 값이 불변임을 보장합니다. ( 프리미티브 타입은 주솟값이 아닌 값을 저장하기 때문에 불변임 )

### 불변객체를 수정해야 한다면 프로퍼티를 수정하는 대신 새로운 객체를 생성해야해요.

```java
class Cash {
    private final int dollars;

    Cash(int val) {
        this.dollars = val;
    }

    public Cash mul(int factor) {
        return new Cash(this.dollars * factor);
    }
}
```

불변 객체는 어떤 방식으로든 자기 자신을 수정할 수 없어요. 항상 원하는 상태를 가지는 새로운 객체를 생성해서 반환해야 해요.

사용법은 아래와 같아요 

```java
Cash five = new Cahs(5);
Cash fifty = five.mul(10);
System.out.println(fifty);
```

일단 five 객체를 생성하고 나면 five는 fifty가 될 수 없어요. 5는 5일뿐이에요. 5의 생명이 다하는 그 순간까지 항상 5에요. 만약 50이 필요하다면 다른 객체를 인스턴스화 해야해요. 

### 가변객체의는 많은 문제를 야기해요. 그렇기에 사용을 엄격하게 금지해야 해요.

### 가변객체가 가지는 문제를 보도록해요. 이를 해결하는 방법이 불변객체에요.

### 1. 식별자 가변성(Identity Mutability)

이 문제는 동일해 보이는 두 객체를 비교한 후 한 객체의 상태를 변경할 때 수면 위로 떠올라요. 

```java
Map<Cash, String> map = new HashMap<>();
        Cash five = new Cash("$5");
        Cash ten = new Cash("$10");
        map.put(five, "five");
        map.put(ten, "ten");
        five.mul(2);
        System.out.println(map);   // {$10 => "five", $10 => "ten"}
```

map안에 동일한 키가 두 개 존재하게 됐어요. 매우 혼란스러운 map이 되었고, 어떠한 결과가 나올지 예측할 수 없어요 

```java
map.get(five);  // "ten"과 "five" 중 하나가 반환될 것이다 
```

### 불변 객체를 사용하면 객체를 map에 추가한 후에는 상태 변경이 불가능하기 때문에 '식별자 가변성' 문제가 발생하지 않아요 .

### 2. 실패 원자성(Failure Atomicity)

완전하고 견고한 상태의 객체를 가지거나 아니면 실패하거나 둘 중 하나만 가능한 특성이에요. (중간은 없어요) 

가변클래스는 이를 구현할 수 없지만, 불변클래스로는 이를 구현할 수 있어요.

```java
class Cash {
	private final int dollars;
	private final int cents;

	Cash(int dollars, int cents) {
		this.dollars = dollars;
		this.cents = cents;
	}

	public Cash mul(int factor) {
		if (/* 뭔가 잘못됨 */) {
			throw new RuntimeException("ooop");
		}
		return new Cash{
			this.dollars * factor,
			this.cents * factor
		}
	}
}
```

가변 객체를 사용하더라도 "실패 원자성"이라는 목표를 달성할 수 있지만, 이를 위해서는 특별한 주의를 기울어야 해요. 크기가 큰 객체라면, 확인하고 복구해야하 할 프로퍼티들이 많기 때문이에요.

### 3. 시간적 결합(Temporal Coupling)

시간적 결합은 로직이 실행되는 순간 순간에 생기는 결합이에요. 

```java
Cash price = new Cash();
price.setDollars(29);
price.setCents(95);
System.out.println(price);	//"$29.95
```

단순한 예제지만 가변 객체를 인스턴스화하고 초기화하는 일반적인 방법을 잘 보여주고 있어요. 

먼저, 모든 private 프로퍼티가 NULL값을 가지도록 '골격(skeleton)'을 만들어요(`인스턴스화`). 그러고 나서 'setter'을 이용해 프로퍼티 값들을 설정해요(`초기화`). 이 방법은 JavaBeans, JPA, JAXB 등의 다양한 표준에서 Java 객체를 조작하기 위해 권장하는 방식이에요. 

이는 '객체 사고(object thinking)'의 관점에서 완전히 잘못된 방식이에요.

위의 Cash클래스는 커다란 데이터 저장소에 몇 개의 프로시저를 추가한 완전한 자바 빈(bean)이에요. 이런 자바 빈 표준을 사용하지 말아요.

### 위와 같이 작성한 코드는 코드의 순서를 프로그래머가 항상 기억해야 해요.

```java
Cash price = new Cash();
price.setDollars(29);
System.out.println(price);	//"$29.00!!
price.setCents(95);
```

위와 같이 잘못된 로직도 실행이 되기 때문이에요.

이를 해결하는 방법은 불변이에요

```java
Cash price = new Cash(29, 95);
System.out.println(price);	//"$29.00!!
```

이제 '항상' 하나의 문장으로도 객체를 인스턴스화 할 수 있게 됐어요. 

이 경우 `인스턴스화`와 `초기화`를 분리시킬 수 없어요. 이 둘은 항상 함께 실행되어야 해요. 

코드가 컴파일되지 않기 때문에, 객체 초기화와 println()의 순서를 변경할 수 도 없어요. 

결국 불변성을 이용해서 구문 사이에 존재하는 시간적 결합을 제거할 수 있게 됐어요. 

객체를 사용해서 어떤 일을 수행하려면 그 전에 객체를 완전한 상태로 초기화해야해요. 그 후에 어떤 일이 일어나는 지는 중요하지 않아요. 객체는 자족적이면서도 견고해요. 더 이상의 초기화는 필요하지 않아요. 

### 4. 부수효과 제거(Side effect-free)

```java
public void print(Cash price) {
		System.out.println("Today price is = " + price);
		price.mul(2);
		System.out.println("Buy now, tomorrow pirce is = " + price);
	}
```

이 메서드를 호출하면 사이트 이팩트가 발생해요 

```java
Cash five new Cash(5):
print(five);
System.out.println(five);	//"$10".. 이런
```

어떤 일이 일어났는지 확인하려면 디버깅 하기까지 많은 시간이 걸릴거에요. 

하지만 Cash를 불변으로 만들면 상태가 변하지 않음을 보장하기에 사이드 이팩트가 생기지 않아요.

Cash의 불변성으로 인해 five가 언제 어디서든 항상 '5달러'를 의미한다고 확신할 수 있기 때문이에요.

### 5. NULL 참조 없애기

```java
class User {
	private final int id;
	private String name = null;

	User(int id) {
		this.id = id;
	}
	
	public void setName(String txt){
		this.name = txt;
	}
}
```

위의 User의 name 프로퍼티는 set으로 초기화 되기전에 null로 유지돼요. 즉 User 클래스를 사용하는 객체들은 User의 name 프로퍼티를 사용하기 전 항상 NULL 체크를 해야해요. 

더큰 문제는 유지보수성과 관련이 있어요. 실제 값이 아닌 NULL을 참조하는 객체는 유지보수성이 저하될 수 밖에 없어요. 언제가 유효한 상태고, 언제 객체가 아닌 다른 형태로 바뀌는 지를 이해하기가 어렵기 때문이에요.

### 해결방법은 모든 객체를 불변으로 만들면 돼요.

모든 객체를 불변으로 만들면 객체 안에 NULL을 포함시키는 것이 애초에 불가능해져요. 다시 말해서 작고, 견고하고, 응집도 높은 객체를 생성할 수 밖에 없도록 강제되기 때문에 결과적으로 유지보수하기에 훨씬 더 쉬운 객체를 만들어용.

### 6. 스레드 안정성(Thread Safety)

스레드 안전성이란 글자 그대로 객체가 여러 스레드에서 동시에 사용될 수 있으며 그 결과를 항상 **예측가능하도록** 유지할 수 있는 객체의 품질을 의미해요. 

아래는 스레드에 안전하지 않은 인스턴스를 생성하는 클래스의 예에요. 

```java
class Cash {
	private int dollars;
	private int cents;

	public void mul(int factor) {
		this.dollars *= factor;
		this.cents *= factor;
	}
}
```

얼핏 보기에는 결함이 없어 보이지만, 두 개의 병렬 스레드 안에서 이 객체를 실행하면 어떤 일이 발생하는 지 살펴볼게요.

```java
Cash price = new Cash("$15.10");
//두 스레드 안에서 다음 뚜 줄울 실행
price.mul(2);
// "$30.20"와 "$60.40"이 예상됨
System.out.println(price);
```

첫 스레드에서 "$30.20"이 된 값이 다음 스레드에서 인자로 넘어가 "$60.40"이 됐어요. 

근데 반복해서 실행해보면 "$60.20"이 결과로 나오는 경우도 있다는 것을 확인할 수 있어요.

`첫 번째 스레드`가 달러와 센트에 각각 2를 곱해요. 동시에 실행되는 `다른 스레드`가 달러에 2를 곱해고 센트에 미처 2를 곱하지 못한 시점에 `첫 번째 스레드`가 printlf()메서드를 실행해요. 이 경우 println()은 "$60.20"을 출력해요. 물론 잠시 후에 두 번째 스레드가 센트에도 2를 곱하겠지만, 짧은 시간 동안은 가격에 '오류가 있는'상태가 유지되요.

### 이또한 해결방법은 불변이에요.

불변 객체는 실행 시점에 상태를 수정할 수 없기 때문에 아무리 많은 스레드가 객체에 접근해도 문제가 없어요. 

명시적인 동기화를 이용하면 가변 클래스 역시 스레드에 안전하게 만들 수는 있어요.

```java
class Cash {
    private int dollars;
    private int cents;

    public void mul(int factor) {
        synchronized (this) {
            this.dollars *= factor;
            this.cents *= factor;
        }
    }
}
```

정상적으로 동작을하겠지만, 하지만 이 방법에는 몇 가지 문제가 있어요. 

첫 번째. 가변 클래스에 스레드 안전성을 추가하는 일은 생각처럼 쉬지 않아요. 

두 번째, 동기화 로직을 추가하는 일은 성능상의 비용을 초래해요. 각각의 스레드가 객체를 사용하기 위해서는 객체가 다른 스레드로부터 해방될 떄 까지 기다려야해요. 각 스레드는 객체를 **배타적으로 잠그기 떄문에** 다른 모든 스레드는 객체가 해제될 때 까지 기다릴 수 밖에 없어요. 또한 데드락이 발생할 수 있어요 .

이런 이유로 가변 객체를 피하고 불변객체를 사용해요.

### 7. 더 작고 더 단순한 객체

### 객체가 단순해질 수록 응집도는 더 높아지고, 유지보수하기는 더 쉬워져요.

### Java에서 허용 가능한 클래스의 최대 크기는 주석과 공백을 포함해서 250줄 정도에요.

250줄을 넘는 클래스는 리팩토링이 필요해요. 

### 클래스가 '작다면' 정확한 줄 수는 중요하지 않아요.

애플리케이션에 포함되어 있는 모든 클래스의 길이를 250줄 이하로 유지할 수만 있다면, 좋은 소프트웨어 개발자이자 아키텍트라고 생각해도 되요. 여기서 말하는 코드란 프로덕션 코드와 테스트 코드 모두를 포함해요.

### 불변 객체를 아주 크게 만드는 일은 불가능하기 때문에, 일반적으로 불변 객체는 가변 객체보다 작아요

`절대로 어떤 클래스도 가변 클래스로 만들지마세요`

## **의견**

그동안 생각했던 불변성을 사용해야하는 이유들은 아주 작은 부분들이었다는 것을 알게됐어요. 

하지만 모든 객체를 불변으로 만들어야 하는건지, 엔티티와 같은 객체는 불변으로 만들지 않아야 하는지, 더 알아봐야겠어요.