## 생성자에 코드를 넣지 마세요.

- 인자에 손대지 말라

- ctor에 코드가 없을 경우 성능 최적화가 더 쉽기 때문에 코드의 실행 속도가 더 빨라진다.

- 인자로 전달된 상태 그대로 캡슐화하고 나중에 요청이 있을 때 파싱 하도록 하여라.

- ctor안에 코드가 있을 경우 후에 리팩토링 하기가 힘들다.

  ```java
  class StringAsInteger implements Number{
  	private String text;
  	public StringAsInteger(String txt){
  		this.text = txt;
  	}
  	public int intValue(){
  		return Integer.parseInt(this.text);
  	}
  }
  ```

  

예고르 형님 말대로 성능 최적화 하는데에 장점이 있을듯! 담에 써봐야겠군...