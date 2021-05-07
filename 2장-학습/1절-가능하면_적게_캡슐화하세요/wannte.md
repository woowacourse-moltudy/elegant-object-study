# 2.1 가능하면 적게 캡슐화하세요
## 내용 정리
| 4개 또는 그 이하의 객체를 캡슐화 해라.
| 상태 없는 객체는 존재해서는 안되고, 상태는 객체의 식별자여야 한다.
equals() 메소드를 오버라이드 해서 사용해라. (@EqaulsAndHashCOde)

# ?
로또를 뽑는 경우 동일한 로또 번호가 나올 가능성이 존재한다.

이러한 경우에는 
```java
class Lotto {
  Long serialNumber;
  LottoNumbers lottoNumbers;
}
```

 같은 형식으로 구분을 해줘야 하나? 아니면 equals를 구현하지 않는 방식으로 진행하는 것이 좋을까? 라는 의문이 든다.
