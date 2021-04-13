# 1.1 -er로 끝나는 이름을 사용하지 마세요
- 클래스는 객체의 팩토리이다. 즉, 클래스가 객체를 인스턴스화한다. 팩토리 패턴은 new 연산자를 확장한 것으로 보아도 좋다. 
- 그렇다면, 클래스의 이름은 어떻게 지어야 할까
	객체를 살아있는 유기체로 본다면, 클래스 이름은 '무엇을 하는지'가 아니라, '무엇인지'에 초점을 두어야 한다.
	보통 명사에 '-er'을 붙일 경우, 절차들의 집합으로 표현될 수 있다. (Validator, Converter 등)

* Public Operation을 통해 외부에서 메시지를 전달하는 것이 익숙하다. 그런 관점에서 Method의 의도를 분명히 드러내도록 [Clean Code](https://kyounghwan01.github.io/blog/etc/how-to-write-clean-code/#%E1%84%92%E1%85%A1%E1%86%B7%E1%84%89%E1%85%AE%E1%84%86%E1%85%A7%E1%86%BC%E1%84%8B%E1%85%B3%E1%86%AB-%E1%84%83%E1%85%A9%E1%86%BC%E1%84%89%E1%85%A1%E1%84%85%E1%85%A9-%E1%84%86%E1%85%A1%E1%86%AB%E1%84%83%E1%85%B3%E1%86%AF%E1%84%85%E1%85%A1)에서 가이드하고 있다. 그러다보니 Class는 명사, Method는 동사를 쓰도록 가이드하고 있다. 하지만 이 책에서는 객체는 '메서드의 집합이 아님'을 강조한다.

```java
object SlackMessageFormatter {
    fun makeRequestReview(reviewPair: ReviewPair, pullRequestView: GithubPullRequestView) =
        {...}

    fun makeRequestChange(reviewPair: ReviewPair, event: PullRequestReviewEvent) =
        {...}

    fun makeMerge(reviewPair: ReviewPair, event: PullRequestEvent, lastReview: String): String {...}
```

* 위와 같이 상태를 가지지 않는 클래스, 인자가 동일할 경우 항상 동일한 결과를 반환하는 함수의 경우에 유틸성 클레스를 작성하곤 했다. 위와 같은 요구사항이 있을 때 SlackMessage란 객체를 도출함으로써 어떤 이점이 있는걸까? 
> http://egloos.zum.com/kwon37xi/v/4844149
