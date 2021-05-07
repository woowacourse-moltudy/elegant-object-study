## 인터페이스를 짧게 유지하고 스마트를 사용하세요

스마트 클래스를 사용하면 높은 응집도를 유지할 수 있다.

```java
interface Exchange {
    float rate(String source, String target);
    final class Fast implements Exchange{
        private final Exchange origin;

        public Fast(Exchange origin) {
            this.origin = origin;
        }

        @Override
        public float rate(String source, String target) {
            final float rate;
            if(source.equals(target)){
                rate = 1.0f;
            }else{
                rate = this.origin.rate(source,target);
            }
            return rate;
        }
        public float toUsd(String source){
            return this.origin.rate(source, "USD");
        }
    }

    final class Smart{
        private final Exchange origin;

        public Smart(Exchange origin) {
            this.origin = origin;
        }

        public float toUsd(String source){
            return this.origin.rate(source, "USD");
        }
        public float eurToUsd(){
            return this.toUsd("EUR");
        }
    }
}

```

이거 어떻게 사용해야될지 잘 모르겠어요...

