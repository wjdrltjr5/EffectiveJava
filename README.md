# EffectiveJava

책 내용 기록

### chapter 2 (객체 생성과 파괴)

-   [생성자에 매개변수가 많다면 빌더를 고려하라](/chapter%202/item2.md)
-   [private 생성자나 열거 타입으로 싱글턴임을 보증하라](/chapter%202/item3.md)
-   [인스턴스화를 막으려거든 private 생성자를 사용하라](/chapter%202/item4.md)
-   [자원을 직접 명시하지 말고 의존 객체 주입을 사용하라](/chapter%202/item5.md)
-   [불필요한 객체 생성을 피해라,다 쓴 객체 참조를 해제하라](/chapter%202/item6%2C7.md)
-   [try-finally 보다는 try-with-resources를 사용하라](/chapter%202/item9.md)

### chapter 3 (모든 객체의 공통 메서드)

Object에서 final이 아닌 메서드는 모두 oveeriding을 염두에 두고 설계된 것이라 재정의 시 지켜야 하는 일반 규약이 명확히 정의되어 있다.

-   [equals는 일반 규약을 지켜 재정의 하라.](/chapter%203/item10.md)
-   [toString을 항상 재정의 하라](/chapter%203/item12.md)
-   clone재정의는 주의해서 진행하라
-   Comparable을 구현할지 고려하라
-   [클래스와 멤버의 접근 권한을 최소화하라](/chapter%203/item15.md)
-   [public 클래스에서는 public 필드가 아닌 접근자 메소드를 사용하라](/chapter%203/item16.md)
-   변경 가능성을 최소화 하라
-   [상속보다는 컴포지션을 사용하라](chapter%203/item18.md)
-   [상속을 고려해 설계하고 문서화하라. 그러지 않았다면 상속을 금지해라](chapter%203/item19.md)
-   [추상클래스 보다는 인터페이스를 우선해라](chapter%203/item20.md)
-   [인터페이스는 구현하는 쪽을 생각해 설계하라.](chapter%203/item21.md)
-   [인터페이스는 타입을 정의하는 용도로만 사용해라](chapter%203/item22.md)
