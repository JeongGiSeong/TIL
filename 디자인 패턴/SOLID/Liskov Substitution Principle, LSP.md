# 리스코프 치환 원칙(Liskov Substitution Principle, LSP)

## 정의
**부모 클래스의 인스턴스 대신 자식 클래스의 인스턴스를 사용해도 동일하게 동작해야 한다**는 원칙.

## 예시: 탈 것
- **LSP 위배 상황:** Vehicle 클래스에 대충 탈 것이니까 직진, 좌회전, 우회전 등의 함수를 만듦. Vehicle를 상속 받아서 Train 기차 클래스를 만들었다면 기차는 좌회전, 우회전을 못하기 때문에 문제 발생.

``` java
public class Vehicle {
    public void GoFoward() { ... }
    public void GoBackward() { ... }
    public void TurnLeft() { ... }
    public void TurnRight() { ... }
}
```

- **해결책:** 이동 담당 인터페이스, 회전 담당 인터페이스를 만들고 조합해서 사용.

``` java
public interface IMovable {
    void GoFoward();
    void GoBackward();
}

public interface ITurnable {
    void TurnLeft();
    void TurnRight();
}

public class RoadVehicle : IMovable, ITurnable {
    public void GoFoward() { ... }
    public void GoBackward() { ... }
    public void TurnLeft() { ... }
    public void TurnRight() { ... }
}

public class Train : IMovable {
    public void GoFoward() { ... }
    public void GoBackward() { ... }
}
```

- **차이점:** 이렇게 하면 Vehicle 클래스를 상속받아도 자식 클래스에서 필요한 메서드만 구현하면 되므로 LSP를 지킬 수 있음.