# 2.7-문서를-작성하는-대신-테스트를-만드세요

## **정리**

### 읽기 쉬운 코드를 만들기 위해서는, 코드를 읽게 될 사람이 비즈니스 도메인, 프로그래밍 언어, 디자인 패턴, 알고리즘을 거의 이해하지 못하는 주니어 프로그래머라고 가정해야해요.

코드를 읽을 사람이 여러분보다 훨씬 더 멍청하다고 가정해야 해요. 이렇게 가정하는 편이 오히려 여러분들의 동료를 존중하는 일이에요.

### 나쁜 프로그래머는 복잡한 코드를 짜요, 훌륭한 프로그래머는 단순한 코드를 짜요.

이상적인 코드는 스스로를 설명하기 때문에 어떤 추가 문서도 필요하지 않아요

```java
Employee jeff = department.employee("Jeff");
jeff.giveRaise(new Cash("$5,000"));
if(jeff.perfomance() < 3.5){
    jeff.fire();
}
```

### 코드를 문서화하는 대신 코드를 깔끔하게(Clean) 만들어요.

단위 테스트 역시 클래스의 일부에요.

단위 테스트는 클래스의 일부이지 독릭적인 객체(Entity)가 아니에요

### 깔끔하고 유지보수 가능한 단위 테스트를 추가하면, 클래스를 더 깔끔하게 만들 수 있고 유지보수성을 향상시킬 수 있어요

한 장의 그림이 수천 단어 만큼의 가치가 있는 것처럼, 하나의 단위 테스트는 한 페이지 분량의 문서 만큼이나 가치가 있어요. 

단위 테스트는 클래스의 사용 방법을 **보여주는데** 반해, 문서는 이해하고 해석하기 어려운 이야기를 들려줘요.

### 프로덕션 코드만큼 단위 테스트에도 관심을 기울여요

### 좋은 예제

```java
class CashTest {
    @Test
    public void summarizes() {
        assertThat(
                new Cash("$5").plus(new Cash("$3")),
                equalTo(new Cash("$8"))
        );
    }
    @Test
    public void deducts() {
        assertThat(
                new Cash("$7").plus(new Cash("-$11")),
                equalTo(new Cash("-$4"))
        );
    }
    @Test
    public void multiplies() {
        assertThat(
                new Cash("$2").mul(3),
                equalTo(new Cash("$6"))
        );
    }
}
```

## **의견**