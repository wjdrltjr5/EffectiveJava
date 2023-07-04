## 상속을 고려해 설계하고 문서화하라. 그러지 않았다면 상속을 금지하라

---

-   메서드를 재정의하면 어떤 일이 일어나느지를 정확히 정리하여 문서로 남겨야 한다. 달리 말하면, 상속용 클래스는 재정의할 수 있는 메서드들을 내부적으로 어떻게 이용하는지(자기사용) 문서로 남겨야 한다.
-   클래스의 api로 공개된 메서드에서 클래스 자신의 또 다른 메서드를 호출할 수도 있다. 그런데 마침 호출되는 메서드가 재정의 가능 메서드라면 그사실을 호출하는 메서드의 api 설명에 적시해야 한다.(더 넓게 말하면 재정의 가능 메서드를 호출할 수 있는 모든 상황을 문서로 남겨야 한다.)
-   api문서의 메서드 설명 끝에서 종종 Implementation Requirements로 시작하는 절을 볼 수 있는데,그 메서드의 내부 동작 방식을 설명하는 곳이다. 이절은 메서드 주석에 @impleSpec 태그를 붙여주면 자바독 도구가 생성해준다.

좋은 api 문서란 어떻게가 아닌 무엇을 하는지를 설명해야 한다.

효율적인 하위 클래스를 큰 어려움 없이 만들 수 있게 하려면 클래스의 내부 동작 과정 중간에 끼어들 수 있는 훅(hook)을 잘 선별하여 protected 메서드 형태로 공개해야 할 수도 있다. 또는, 드물게는 protected 필드로 공개해야 할 수도 있다.

상속용 클래스를 시험하는 방법은 직접 하위클래스를 만들어보는 것이 유일하다.

널리 쓰일 클래스를 상속용을 설계한다면 여러분이 문서화한 내부 사용패턴과, protected 메서드와 필드를 구현하면서 선택한 결정에 영원히 책임져야 한다. 그러니 상속용으로 설계한 클래스는 배포 전에 반드시 하위 클래스를 만들어 검증해야 한다.

상속용 클래스의 생성자는 직접적으로든 간접적으로든 재정의 가능 메서드를 호출해서는 안된다.

```java
public class Super {
    // 잘못된 예 - 생성자가 재정의 가능 메서드를 호출한다.
    public Super() {
        overrideMe();
    }

    public void overrideMe() {

    }
}
public class Sub extends Super {

    private final Instant instant;

    Sub() {
        instant = Instant.now();
    }

    // 재정의 가능 메서드. 상위 클래스의 생성자가 호출한다.
    @Override
    public void overrideMe() {
        System.out.println(instant);
    }

    public static void main(String[] args) {
        Sub sub = new Sub();
        sub.overrideMe();
    }
}

// 이프로그램이 instant를 두 번 출력하리라 기대했겠지만 , 첫 번째는 null을 출력한다. 상위클래스의 생성자는 하위 클래스의 생성자가 인스턴스 필드를 초기화 하기도 전에 overrideMe를 호출하기 때문이다.
```

clone과 readObject 모두 직접적으로든 간접적으로든 재정의 가능 메서드를 호출해서는 안 된다.

---

상속용 클래스를 설계하기란 결코 만만치 않다. 클래스 내부에서 스스로를 어떻게 사용하는지(자기사용 패턴 ) 모두 문서로 남겨야 하며, 일단 문서화한 것은 그 클래스가 쓰이는 한 반드시 지켜야 한다. 그러지 않으면 그 내부 구현 방식을 믿고 활용하던 하위 클래스를 오동작하게 만들 수 있다. 다른 이가 효율 좋은 하위 클래스를 만들 수 있도록 일부 메서드를 protected로 제공해야 할 수도 있다. 그러니 클래스를 확장해야 할 명확한 이유가 떠오르지 않으면 상속을 금지하는 편이 나을 것이다. 상속을 금지하려면 클래스를 final로 선언하거나 생성자 모두를 외부에서 접근할 수 없도록 만들면 된다.