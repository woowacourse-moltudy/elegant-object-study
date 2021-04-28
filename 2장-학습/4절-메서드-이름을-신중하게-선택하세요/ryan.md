## 메서드의 이름을 신중하게 선택하세요

- 빌더(새로운객체반환)의 이름은 명사로, 조정자(수정하는메서드)의 이름은 동사로
- 형용사를 추가해서 빌더의 이름이 나타내는바를 더 명확히
- 부사를 추가해서 조정자의 이름이 나타내는바를 더 명확히



#### 2.4.1 빌더는 명사다

필자의 주장 : 잘못된 예시

```java
class Bakery{
	Food cookBrownie();
	Drink brewCupOfCoffee(String flavor);
}
```

실 사용에서는 `Food something = parisBakery.cookBrownie()`

이거는 이상한 느낌이 있긴 하다. 해석하면 빠바 브라우니 요리하다.





필자가 주장: 좋은 예시

```java
class Bakery{
	Food cookedBrownie();
	Drink brewedCupOfCoffee(String flavor);	
}
```

실 사용에서는 `Food something = parisBakery.cookedBrownie()`

내가 보긴 이거도 이상하다. 해석하면 빠바 요리된 브라우니.



마이 아이디어:

`Food something = parisBakery.getCookedBrownie()`

내 생각엔 이게 더 자연스러운데? 빠바에서 요리된 브라우니를 받다.

내 생각엔 예고르형님 아이디어 + 게터를 추가시키면 더 자연스러운 문장이 탄생함.(게터+(형용사)+명사형)



#### 2.4.2 조정자는 동사다

조정자는 동사를 써라

빌더패턴도 쓰지말라함.



#### 2.4.3 빌더와 조정자 혼합하기

혼합해서 사용하지 마라



#### 2.4.4 Boolean 값을 결과로 반환하는 경우

`isExists()` 는 잘못됬고 `exists()` 가 맞다

`isEmpty()` 는 잘못됬고 `empty()`가 맞다

라고 주장한다.

내 생각에도 확실히 동사+동사 조합은 이상하다.

하지만 동사+형용사 조합은 자연스럽다고 생각한다.

`yourName.empty();`

그래ㅏ, 뭐 이상하지는 않은데...

`yourName.isEmpty();`

이게 더 낫지 않나?

`your name is empty?`

`your name empty?`

음....

원래 영어에서도 

뒷부분 발음만 살짝 올려 말하면 의문문이 된다.

이것도 그렇게 생각햇을때 is 가 잇는것이 더 읽기 좋음.





`if(name.emptiness() == true)`

이것을 `if emptiness **of the ** name is true `이렇게 읽으면 자연스럽다는데..

`if(name.isEmpty() == true)`

나는 `if yourname is empty? True` 이게 더 자연스럽게 읽힌다.



of the 를 무의식적에 붙여 읽는거는 좀 아니자나~~~







