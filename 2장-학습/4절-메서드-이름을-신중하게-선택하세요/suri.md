# 2.4 메서드 이름을 신중하게 선택하세요.

- 빌더의 이름은 명사로 조정자의 이름은 동사로 지어라
- 빌더란 뭔가를 만들고 새로운 객체를 반환하는 메서드
- 조정자는 객체로 추상화한 실세계 엔티티를 수정하는 메서드



- 뭔가를 조작한 후 반환하거나 뭔가를 만드는 동시에 조작하는 메서드가 있어서는 안됨
  - 메서드는 빌더나 조정자 둘중 하나여야 한다.
- Boolean을 반환하는 경우는 이름을 형용사로 지어야 한다.



# 느낀점

언젠가 "지금까지 메소드는 동사로 시작해야 한다." 라는 말을 듣고 부터 메소드 이름은 동사로 시작하려고 하였다.

그러나 이번 챕터를 읽으면서 빌더와 조정자라는 개념에 대해 알게 되었다. 실생활에서 처럼 정말 객체에게 자율성을 주는 듯한 느낌이 들었다.

앞으로는 해당 챕터에서 읽은 내용을 사용해 봐야 겠다.





