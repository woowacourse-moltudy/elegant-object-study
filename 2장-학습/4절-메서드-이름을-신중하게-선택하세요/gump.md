
# 2.4 -메서드 이름을 신중하게 선택하세요

## **정리**

### 빌더는(Builder)의 이름은 명사로, 조정자(manipulator)의 이름은 동사로 지어요.

### **빌더(builder)**

빌더란 뭔가를 만들고 새로운 객체를 반환하는 메서드를 가르켜요.

빌더는 항상 뭔가를 반환해요. 

빌더의 반환 타입은 절대 void가 될 수 없으며,

이름은 항상 명사여야 해요

### 빌더 예제

```java
int pow(int base, int power);
float speed();
Employee employee(int id);
String parsedCell(int x, int y);
```

마지막 메서드인 parsedCell()을 보면, 형용사인 parsed가 명사인 cell을 꾸미는 형태를 취하고 있어요. 이러한 방식은 앞에서의 원칙(빌명조동)을 위반하지 않아요. 오히려 의미를 풍부하게 해주니, 이 메서드가 어떤 형태로든 cell의 원래 내용을 변환한 후 반환할 것이라는 사실을 기대할 수 있어요. 

<br>

### **조정자(manipulator)**

객체로 추상화한 실세계 엔티티를 수정하는 메서드를 가르켜요. 

조정자의 반환타입은 항상 void이고,

이름은 항상 동사여야 해요.

### **조정자 예제**

```java
void save(String content);
void put(String key, Float value);
void remove(Employee emp);
void quicklyPrint(int id);
```

마지막 메서드인 quicklyPrint()를 보면, 부사인 quickly가 동사인 print를 꾸며주고 있어요. 이 또한 동사에 풍부한 의미를 사용하니 원칙에 위배되지 않아요.

### **잘못된 예제**

```java
int save(String content);  
boolean put(String key, Float value);
float speed(float val);  //빌더인 동시에 조정자이기 때문에 잘못됨
```

save메서드는  조정자이기 때문에 잘못됐어요, void를 반환하거나 bytesSaved()로 변경해야해요.

put 메서드는 조정자처럼 동작하지만 빌더처럼 boolean을 반환하기에, 잘못됐어요. PutOperation 인스턴스를 반환해 클래스의 전반적인 설계를 수정해야해요.  즉, PutOperation 클래스는 조정자인 save()메서드와 성공/실패 여부를 반환하는 빌더인 success()메서드를 포함할 것입니다. 

speed 메서드 또한 빌더인 동시에 조정자에요. put메서드와 마찬가지로 SaveSpeed 클래스를 추가하도록 해요 .

### **빌더는 객체로부터 뭔가를 얻기를 바랄 때 사용해요.**

즉, 우리는 객체로부터 뭔가를 얻어요. 다시 말해 뭔가를 만들라고 객체에게 요청해요. 어떻게 줄지는 요청한 객체가 알아서 하도록 맡겨요.

### **메서드의 이름을 동사로 지을 때에는 객체에게 "어떻게 할지"가 아닌,  "무엇을 할 지"를 알려줘야해요.**

어떻게, 만들라고 요청하는 것은 협력자에 대한 존중이 없을 뿐더러 예의에도 어긋나는 방식이에요.

무엇을 만들어야 하는 지만 요청하고, 만드는 방법은 객체 스스로 결정하도록 해야해요. 

### **조정자는 객체에게 일을 하도록 지시하지만, 얻기를 바라진 않아요.**

오직 빌더만이 값을 반환할 수 있고 이때 빌더의 이름은 명사에요. 객체가 뭔가를 조정해야 한다면 이름은 동사이고 반환값은 없어요. 

### **빌더와 조정자가 혼합되어 있는 경우 클래스를 하나더 만들어요.**

```java
class Document {
	int write(InputStream content);    //잘못됨(빌더와 조정자를 혼합)
}
```

위와 같이 정의되어있다 할 때,

아래와 같이변경 할 수 있어요.

```java
class Document {
	OutputPipe output();
}

class OutputPipe {
	void write(InputStream content);
	int bytes();
	long time();
}
```

### Boolean은 값을 반환하기 때문에 빌더에 속하지만, 가독성 측면에서 형용사로 지어요.

```java
boolean empty();  //is empty
boolean readable();  //is readable
boolean negative();  //is negative
```

메서드를 읽을때 is 가 붙어있다고 생각하고 읽어요. 

```java
boolean equals(Object obj);
boolean exists();
```

위와 같은 메서드에서는 문제가 될 수 있어요. is를 붙이면 isEquals와 isExists라는 올바르지 않은 문장이 만들어 지기 때문이에요.

```java
boolean equalTo(Object obj);
boolean present();
```

위와 같이 짓기로 해요. 

### 메서드는 빌더나 조정자, 둘중 하나여만 해요. 결코 빌더인 동시에 조정자여서는 안되요.

빌더는 명사로, 조정자는 동사로 이름을 지어요. 

Boolean값을 반호나하는 빌더는 예외에요 이때는 형용사로 지어요. 이게 끝이에요. 

## **의견**

개발을 하다보면 네이밍을 항상 신경써야해요. 이러한 고민하는 시간 줄일 수 있게 빌더, 조정자, boolean으로 정형화 했다는 점은 좋은 방법이에요.

하지만 클린코드에서 제시한, 제가 이전에 주로 사용했던(메서드 이름은 동사, 변수이름은 명사, 클래스 이름은 명사 ), 네이밍 방법과는 또 다른 방법이라, 거부감이 약간 들어요.  

이 괴리감을 줄이는게 먼저 선행되야 할 것 같아요.