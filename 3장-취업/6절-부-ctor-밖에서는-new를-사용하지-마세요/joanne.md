# 3.6 부 ctor 밖에서는 new를 사용하지 마세요.

토비의 스프링에서도 비슷한 내용을 봤다.
생성되는 부분을 특정 객체 내부에서 하게 된다면 의존성을 갖게 된다. 
여기서도 부 ctor 밖에서는 New를 사용하지 말라는 뜻이, 특정 객체를 생성할 때 필요한 것을 의존성 주입을 통해 해결해야하며 내부 메서드에서 연관 관계를 갖고 있지 마라는 뜻인 듯?
이렇게 되면 관심사의 변화가 생겼을 때 확장하기 용이할 것이다.

