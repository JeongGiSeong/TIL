# 인터페이스 분리 원칙(Interface Segregation Principle, ISP)

## 정의
**인터페이스를 사용할 때 한 번에 크게 만들지 말고, 작은 단위로 쪼개어 만들어야 한다**는 원칙. 

## 예시: 유닛 스테이터스 관련 인터페이스
- **ISP 위배 상황:** 유닛 클래스에 동작, 상태 관련 함수를 모두 넣음.
```java
public class Unit {
    void Health() { ... }
    void Strength() { ... }
    void GoForward() { ... }
    void Attack() { ... }
}
```
- **해결책:** 동작, 상태 관련 인터페이스와 상태 관련 인터페이스로 나누고 조합해서 사용.
```java
public interface IUnitStatus {
    void Health();
    void Strength();
}

public interface IUnitAction {
    void GoForward();
    void Attack();
}

public class Unit : IUnitStatus, IUnitAction {
    public void Health() { ... }
    public void Strength() { ... }
    public void GoForward() { ... }
    public void Attack() { ... }
}
```

## 장점
- 인터페이스가 단순하고 명확해지며, 클라이언트가 필요로 하는 기능에만 집중할 수 있음.
- 불필요한 의존성을 제거하여 코드의 결합도를 낮출 수 있음.
- 변경에 대한 영향을 최소화하고, 유연하고 확장 가능한 코드를 작성할 수 있음.