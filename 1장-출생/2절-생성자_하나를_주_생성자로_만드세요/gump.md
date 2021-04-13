# **1.2 생성자 하나를 주 생성자로 만드세요**

## **정리**

### **2~3개의 메서드와 5~10개의 생성자를 가지는 클래스를 만드세요**

메서드의 수보다 생성자의 수가 더 많아야 응집도가 높고 견고한 클래스를 만들 수 있어요.

### **주 생성자 1개 나머지는 부생성자로 만드세요**

```java
class Cash {
		private int dollars;
		
		Cash(float dollars) {
			this((int) dollars);
		}

		Cash(String dollars) {
			this(Cash.parse(dollars));
		}

		Cash(int dollars) {
			this.dollars = dollars;
		}
}
```

중복 코드를 방지하고 설계를 더 간결하게 해줘요.

## **의견**

이 원칙이 완벽하다면, 왜 자바 구현체들은 적은 수의 생성자와 많은 수의 메서드를 가질까..?