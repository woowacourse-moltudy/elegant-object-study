## 2.9-인터페이스를-짧게-유지하고-스마트(smart)를-사용하세요

## 정리

### 클래스가 다수의 인터페이스를 구현하기 때문에 인터페이스를 작게 만드는 것은 클래스를 작게 만드는 것보다 훨씬 중요해요.

```java
interface Exchange {
    float rate(String target);
    float rate(String origin, String target);
}
```

이 인터페이스는 너무 많은 것을 **요구하기** 때문에 설계 관점에서는 형편 없는 인터페이스에요.

인터페이스는 고현 클래스가 준수해야 하는 계약이에요. 현재 위의 인터페이스는 구현자에게 너무 많은 것을 요구하기에. 이런 종류의 계약은 단일 책임 원칙(Single Responsibility Principle)을 위반하는 클래스를 만들도록 부추겨요.

하나의 인자를 받는 rate() 메서드는 이 인터페이스에 포함되어서는 안돼요.

이를 해결하기 위해서 필요한 것이 **'스마트(smart)'클래스**에요.

```java
interface Exchange {
    float rate(String origin, String target);

    final class Smart {
        private final Exchange origin;

        public Smart(Exchange origin) {
            this.origin = origin;
        }

        public float toUsd(String source) {
            return this.origin.rate(source, "USD");
        }
    }
}
```

이러한 '스마트'클래스는 아주 명확하고 공통적인 작업을 수행하는 많은 메서드들을 포함할 수 있어요. 이 '스마트'클래스는 Exchange 인터페이스가 어떻게 구현되고 환율이 어떻게 계산되는지는 모르지만, 인터페이스 위에 특별한 기능을 적용해요. 

이 기능은 Exchange의 서로 다른 구현 사이에 공유될 수 있어요. 

### 스마트 클래스를 인터페이스와 함께 제공해야 하는 또 다른 이유는 인터페이스를 구현하는 서로 다른 클래스 안에 동일한 기능을 반복해서 구현하고 싶지 않기 때문이에요

요구사항이 추가되어 USD를 EUR로 변환을 해야하는 기능을 추가해야한다면, 이는 인터페이스에 추가하는 것이 아닌, '스마트'클래스에 추가하는 것이 좋아요.

```java
float rate = new Exchange.Smart(new NYSE())
                .toUsd("EUR");
```

환율 변환이 필요한 모든 위치에서 'EUR'이라는 문자열 리터럴을 반복적으로 사용하고 싶지는 않아요. 이때 필요한 것은 USD를 EUR로 변환해주는 eurToUsd()메서드에요 

```java
interface Exchange {
    float rate(String origin, String target);

    final class Smart {
        private final Exchange origin;

        public Smart(Exchange origin) {
            this.origin = origin;
        }

        public float toUsd(String source) {
            return this.origin.rate(source, "USD");
        }
        
        public float eurToUsd() {
            return this.toUsd("EUR");
        }
    }
}
```

이제 단 한번의 메서드 호출만으로 EUR에서 USD로의 환율을 얻을 수 있어요.

```java
float rate = new Exchange.Smart(new NYSE())
                .eurToUsd();
```

### '스마트'클래스의 크기는 점점 더 커지겠지만, Exchange 인터페이스는 작고, 높은 응집도를 유지할 수 있어요.

인터페이스에는 오직 하나의 메서드만 선언하고, NYSE, XE, Yahoo 등의 환율 제공자는 이 메서드를 구현애요. 

모든 거래소들이 기능을 공유할 수 있기 때문에 각 거래소들이 해당 기능을 개별적으로 구현할 필요가 없어요. 

이것이 바로 이번 섹션의 제목과 주제를 "인터페이스를 짧게 유지하세요"로 정한 이유에요. 

### 스마트 클래스는 네트워크 호출에 대한 어떤 것도 알아서는 안돼요

### 기본적으로 인터페이스를 짧게 만들고 '스마트' 클래스를 인터페이스와 함께 배포함으로써 공통 기능을 추출하고 코드 중복을 피할 수 있어요.

### 예제

[https://github1s.com/jcabi/jcabi-github/blob/HEAD/src/main/java/com/jcabi/github/Blob.java](https://github1s.com/jcabi/jcabi-github/blob/HEAD/src/main/java/com/jcabi/github/Blob.java)

## 의견

앞 절의 Fake 객체는 테스트를 간소화 하기에 필요하고, 테스트의 의미를 더 강하게 해주기에 그 의미가 잘 다가왔어요.

하지만 이번 절의 Smart클래스는 한번도 사용하지 않아서 그런지 쉽게 이해가 되지않아요.                                                                                                                                                                                                                     

인터페이스에 기능을 추가하지 않고, 인터페이스 내부의 클래스에 그 기능을 추가하는게 어떤 효과가 있는지. 어려워요. 중복을 줄이기 위해 과한 설계가 요구되는게 아닌가 싶어요.