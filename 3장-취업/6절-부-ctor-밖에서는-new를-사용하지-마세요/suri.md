# 부 ctor 밖에서는 new를 사용하지 마세요

- 하드코딩 된 의존성
  - Cash 클래스는 Exchange 클래스에 직접 연결되어 있기 때문에 의존성을 끊기 위해서는 Cash 클래스의 내부 코드를 변경할 수 밖에 없다.

```Java
class cash {
	private final inte dollars;
	
	public int euro() {
		return new Exchange().rate("USD", "EUR") * this.dollars; 
	}
}
```



- Cash의 테스트를 한다면? Exchange()가 서버의 통신하는 기능과 같은 일을 한다면?
  - Cash를 테스트 할 때 다른 Exchange를 쓰고 싶어..!

```java
class cash {
	private final int dollars;
	
	Cash() {
		this(0);
	}
	
	Cash(int value) {
		this(value, new NYSE());
	}
	
	Cash(int value, Exchange exch) {
		this.dollars = value;
		this.exhange = exch;
	}
	
	public int euro() {
		return this.exchange.rate("USD", "EUR") * this.dollars;
	}
}
```



- 부 생성자를 제외한 어떤 곳에서도 new를 사용하지 마세요.

```java
class Request {
	private final Socket socket;
	
	public Request(Socket socket) {
			this.socket = skt;
	}
	
	public Request next() {
		return new SimpleRequest(/* 소켓에서 데이터를 읽는다. */)
	}
}
```



- next()에서 사용하는 new를 없애려면

```java
class Requests {
	private final Socket socket;
	private final Mapping<String, Request> mapping;
	
	public Requests(Socket socket) {
		this(skt, new Mapping<String, Request>() {
			@Oberride
			public Request map(String data) {
				return new SimpleRequest(data);
			}
		})
	}
}
```



# 느낀점

- interface를 통한 의존성 주입은 너무 멋진 것 같다!!
  - 유연성이 늘어나는게 보임

