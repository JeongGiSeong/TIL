# DIP(Dependency Inversion Principle)

## 정의
고수준 모듈은 저수준 모듈에 의존해서는 안 되며, 둘 모두 추상화에 의존해야 한다는 원칙입니다. 즉, 구체적인 구현에 의존하는 것이 아니라 인터페이스나 추상 클래스에 의존해야 합니다.

## 예시: 문, 스위치
- **DIP 위배 상황:** 문이 스위치에 의존하고 있음. Switch 클래스는 Door를 직접 참조하고 있어서 Door 클래스**만** 사용할 수 있음. 하지만 Switch는 Door 대신 다른 장치를 사용할 수 있어야 함.
```java
public class Door {
    public void Open() { ... }
    public void Close() { ... }
}

public class Switch {
    private Door door;
    private boolean isActivated;

    public Toggle(Door door) { ... }
}
```

- **해결책:** 추상화된 인터페이스를 만들어서 사용. 이러면 Switch 클래스는 Door 클래스 뿐만 아니라 ISwitchable 인터페이스를 사용하는 다른 장치도 사용할 수 있음.
```java
public interface ISwitchable {
    public void Activate();
    public void Deactivate();
}

public class Door implements ISwitchable {
    public void IsActivated() { ... }
    public void Activate() { ... }
    public void Deactivate() { ... }
}

public class Switch {
    private ISwitchable client;

    public Toggle() {
        if (client.IsActivated()) {
            client.Deactivate();
        } else {
            client.Activate();
        }
     }
}
```

- **차이점:** 특정 클래스에 직접 의존하는 게 아니라 인터페이스를 거쳐서 사용하므로 느슨한 결합을 유지할 수 있음.

## 장점
- **유연성:** 구체적인 구현이 아닌 추상화에 의존하므로 구현이 변경되어도 영향을 최소화할 수 있음.
- **테스트 용이성:** 의존성을 주입하여 테스트하기 쉬워짐.
- **확장성:** 새로운 구현을 추가하기 쉬워짐.
- **유지보수성:** 변경에 대한 영향을 최소화할 수 있음.