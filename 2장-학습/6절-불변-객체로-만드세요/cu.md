# 2.6 불변 객체로 만드세요

> https://brainbackdoor.tistory.com/141


### 불변객체 이점

1. 불변 객체를 사용하면 식별자 가변성 문제가 발생하지 않는다. 가령 아래와 같이 Map을 사용할 때 요소의 상태를 변화시켜 키를 중복상태로 만들 수 있다.

```java
Map<Cash, String> map = new HashMap();
Cash five = new Cash("$5");
Cash ten = new Cash("$10");
map.put(five, "five");
map.put(ten, "ten");
five.multiple(2);
System.out.println(map); // {$10=>"five", $10=>"ten"}
```

2. 불변객체를 사용하면 실패원자성을 확보할 수 있다. 즉, 견고한 객체이거나 실패하거나 두가지 경우만 존재한다.

3. 시간적 결함을 제거할 수 있다. 객체의 상태를 변경시키는 시점에 따라 결과가 달라지는 경우, 데이터의 흐름을 머릿속에 그려가며 프로그래밍을 해야 한다. 이런 절차지향적인 사고를 막을 수 있다.

```java
Cash price = new Cash();
// 50 줄의 코드
price.setDollars(29);
System.out.println(price); // "$29.00"
// 30 줄의 코드
price.setCents(95);
System.out.println(price); // "$29.95"
```

4. Side effect를 제거할 수 있다. 이는 Thread safe와 함께 생각해봐도 좋다. Multi Thread 환경에서 공유가변데이터가 존재할 경우 동기화처리가 제대로 되지 않으면 여러 부수효과가 발생할 수 있다. 이걸 모두 생각하며 프로그래밍하는 것보다는 불변객체를 사용하는 것이 실용적이다.

5. 불변객체를 사용하여 인스턴스화할 때 상태를 초기화하도록 강제하면, NULL 참조를 할 수 없어 좋은 설계를 유도할 수 있다.

- 단순함을 보다보니 심플 소프트웨어가 떠오른다..
> http://www.yes24.com/Product/Goods/80749963
