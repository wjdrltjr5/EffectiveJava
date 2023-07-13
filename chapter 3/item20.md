## 추상클래스 보다는 인터페이스를 우선해라

---

자바8부터는 인터페이스도 디폴트 메서드를 제공할 수 있게 되어 인터페이스와 추상클래스 모두 인스턴스 메서드를 구현 형태로 제공할 수 있다. 둘의 가장 큰 차이는 추상클래스가 정의한 타입을 구현하는 클래스는 반드시 추상 클래스의 하위 클래스가 되어야 한다. 자바는 단일 상속만 지원하니 커다란 제약을 안게 되는 셈이다.

장점들

-   기존 클래스에도 손쉽게 새로운 인터페이스를 구현해 넣을 수 있다.(기존클래스에 새로운 추상 클래스를 끼워 넣기는 어려움 두 클래스가 같은 추상 클래스를 확장하려면 그 추상클래스는 계층 구조상 두 클래스의 공통조상이어야 한다.)

-   인터페이스는 믹스인 정의에 안성맞춤이다.(믹스인이란 클래스가 구현할 수 있는 타입으로 원래의 주된타입 외에도 특정 선택적 행위를 제공한다고 선언하는 효과를 준다.
    ex. Comparable을 구현한 클래스의 인스턴스끼리는 순서를 정할 수 있다고 선언하는 믹스인 인터페이스.)

-   인터페이스로는 계층 구조가 없는 타입 프레임워크를 만들 수 있다.(ex. 가수인터페이스,작곡가인터페이스가 있을때 가수겸 작곡가)

-   래퍼클래스 관용구(아이템18)와 함께 사용하면 인터페이스는 기능을 향상시키는 안전하고 강력한 수단이 된다.(타입을 추상 클래스로 정의해두면 그 타입에 기능을 추가하는 방법은 상속 뿐이다. 상속해서 만든 클래스는 래퍼 클래스보다 활용도가 떨어지고 깨지기는 쉽다.)

-   인터페이스의 메서드 중 구현 방법이 명확한 것이 있다면 디폴트메소드로 제공하는 것이 좋다.

-   인터페이스와 추상 골격 구현 클래스를 함께 제공하는 식으로 인터페이스와 추상 클래스의 장점을 모두 취하는 방법도 있다.(인터페이스로는 타입을 정의하고, 필요하면 디폴트 메서드 몇 개도 함께 제공, 골격 구현 클래스는 나머지 메소드들까지 구현한다. 이렇게 해두면 단순히 골격 구현을 확장하는 것만으로 이 인터페이스를 구현하는 데 필요한 일이 대부분 완료된다.(템플릿메소드패턴))

-   단순 구현(simple implementation)은 골격 구현의 작은 변종으로 상속을 위해 인터페이스를 구현한 것이지만, 추상 클래스가 아니란 점이 다르다 쉽게 말해 동작하는 가장 단순한 구현이다.(그대로 써도 되고 필요에 맞게 확장해도 됨)

---

일반적으로 다중 구현용 타입으로는 인터페이스가 가장 적합하다. 복잡한 인터페이스라면 구현하는 수고를 덜어주는 골격 구현을 함께 제공하는 방법을 꼭 고려해보자. 골격 구조현은 가능한 한 인터페이스의 디폴드 메서드로 제공하여 그 인터페이스를 구현한 모든 곳에서 활용하도록 하는 것이 좋다. 가능한 한 이라고 한 이유는 , 인터페이스에 걸려있는 구현상의 제약 때문에 골격 구현을 추상 클래스로 제공하는 경우가 더 흔하기 때문이다.