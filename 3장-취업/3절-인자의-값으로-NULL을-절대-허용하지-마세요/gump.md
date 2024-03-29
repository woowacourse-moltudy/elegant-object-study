# **3.3-인자의 값으로 NULL을 절대 허용하지 마세요**

## **정리**

### **이번 장에선 메서드의 인자값으로 NULL을 사용하는 경우를 살펴볼거에요**

NULL을 허용하는 find() 메서드를 구현하기 위해서는 다음과 같이 분기를 처리할 필요가 있어요 

```java
public Iterable<File> find(String mask) {
    if (mask == null) {
        //모든 파일을 찾는다.
    } else {
        // 마스크를 사용해서 파일을 찾는다. 
    } 
}
```

여기서 문제가 되는 부분은 mask == null 이에요. 이는 mask 객체에게 이야기하는 대신, 이 객체를 **피하고 무시해요.** 말 그대로 객체의 면전에 대고 "당신과 이야기 나눌 가치가 있나요?" 또는 "그 객체에게 말할 가치가 있나요?"라고 묻는 것이에요. 

심지어 객체에게 직접 이야기하지도 않아요. 그 객체가 충분히 좋은지 아닌지를 객체를 알고 있을 것으로 추측되는 누군가에게 물어요.(예의 없는 사람이네요)

### **객체를 존중한다면 아래와 같이 행동해야해요**

```java
public Iterable<File> find(Mask mask) {
    if (mask.empty()) {
        //모든 파일을 찾는다.
    } else {
        // 마스크를 사용해서 파일을 찾는다.
    }
}
```

더 개선한다면 아래와 같아요

```java
public Iterable<File> find(Mask mask) {
    Collection<File> files = new LinkedList<>();
    for (File file : files) {
        if (mask.matches(file)) {
            file.add(file);
        }
    }
    return files;
}
```

### **mask 객체를 존중한다면 조건의 존재 여부를 객체 스스로 결정하게 해야해요.**

겉모습만으로 객체를 판단해서 안돼요. 

### **인자의 값에 NULL을 허용하면 mask==null같은 비교문을 사용할 수 밖에 없어요**

이는 절차지향의 유산을 가져온 것이에요.

역참조란 메모리의 실제 값을 참조하는 것이에요. ( **p )

데이터를 조작하는 절차적인 프로그래밍에서는 **바보같은 데이터**만 사용하기에 **역참조**를 사용해야 하지만, Java에서는 필요가 없어요.

그렇기에 여전히 null이 존재해야하는 이유는 전혀 없어요. (저자는 커다란 실수라고 말해요)

### **OOP에서 존재하지 않는 인자(absent argument) 문제는 널 객체(null object)를 이용해서 해결해야해요**

전달할 것이 없다면, 비어있는 것처럼 행동하는 객체를 전달하면 돼요.

```java
interface Mask {
    boolean matches(File file);
}
```

Mask 인터페이스의 적절한 구현은 글롭패턴( '*.txt'형식의 패턴, 나중에 알아보자)을 캡슐화하고 이 패턴에 대해 파일 이름을 매칭시킬 거에요. 반면에 Null 객체는 다음과 같이 구현 할 수 있어요.

```java
class AnyFile implements Mask {
    @Override
    public boolean matches(File file) {
        return true;
    }
}
```

AnyFile은 Mask의 특별한 경우로, 어떤 내부 로직도 포함하지 않아요. 어떤 파일을 전달하더라도 항상 true를 반환해요. 

이제 Null 값을 전달하는 대신, AnyFile의 인스턴스를 생성해서 find()메서드에 전달하면돼요. 

find()메서드는 무슨 일이 일어나고 있는지 전혀 알지 못한 채, 여전히 올바른 Mask가 전달되었다고 생각할 거에요.

### **Null을 무조건 써야할 때 대응법**

### **1. 방어적인 방법으로, NULL을 체크한 후 예외를 던짐**

### **2. NULL을 가볍게 무시함**

인자가 절대 NULL이 아니라고 가정하고 어떤 대비도 하지 않아요. 메서드를 실행하는 도중에 인자에 접근하면 NullPointerException이 던져지고 메서드 호출자는 자신이 실수했다는 사실을 인지해요

### **요약, 메서드 인자로 절대로 NULL을 사용하지마세요**

## **의견**

Null의 대응법이 조금 웃겼다. 

실제 현업에서도 가볍게 무시할 수 있는지가 의문이긴하다.. 

(예고르 행님이 아무리 확고한 생각을 가지고 있어도 모두를 이해시킬 순 없었나보다)