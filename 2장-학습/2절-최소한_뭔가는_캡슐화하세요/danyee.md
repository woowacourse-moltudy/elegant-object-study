# 2.2 최소한 뭔가는 캡슐화하세요

## 정리
- 아무것도 캡슐화하지 않는 방식은 바람직하지 않다.

```
class Year {
    int read() {
        return System.currentTimeMillis() / (1000 * 60 * 60 * 24 * 30 * 12) - 1970;
    }
}
```
<br/>

- 순수한 OOP에서는 정적 메소드가 존재하지 않기 때문에 정적 메소드를 호출하는 일이 불가능하다.
- 대신 어떤 클래스의 인스턴스를 생성한 후 이 인스턴스를 통해 값을 얻어야 한다.

```
class Year {
    private Millis millis;

    Year(Millis msec) {
        this.millis = msec;
    }

    int read() {
        return this.millis.read() / (1000 * 60 * 60 * 24 * 30 * 12) - 1970;
    }
}
```

## 느낀점

- 유틸성 클래스는 객체지향을 위반한다고 생각한다.
- 객체는 다른 객체와 협력하기 때문에 최소한 하나라도 캡슐화해야 한다는 의견에 동의한다.