# 개방-폐쇄 원칙(Open-Closed Principle, OCP)

## 정의
**클래스는 확장에 대해서는 개방적이고, 수정에 대해서는 폐쇄적이어야 한다**는 원칙

## 예시: 도형 그리기
- **OCP 위배 상황:** 도형의 넓이를 계산하는 Calculator 클래스가 각 도형별로 계산식을 가지고 있는 경우. 예를 들어, GetRectangleArea 메서드와 GetCircleArea 메서드가 있을 때, 새로운 도형의 넓이를 계산하려면 Calculator 클래스를 수정해야 함.
``` java
public class Calulator {
    public float GetRectangleArea(Rectangle retangle) {
        return retangle.width * retangle.height;
    }
    public float GetCircleArea(Circle circle) {
        return circle.radius * circle.radius * Mathf.PI;
    }
}
```
- **해결책:** Shape라는 추상 클래스를 만들고, 넓이를 계산하는 CalculateArea라는 추상 메서드를 정의. 그리고 Rectangle과 Circle 클래스는 Shape 클래스를 상속받아 CalculateArea 메서드를 오버라이드. 이렇게 하면 새로운 도형이 추가되더라도 Shape를 상속받아 해당 도형의 넓이를 계산하는 메서드만 구현하면 됨.
``` java
public abstract class Shape {
    public abstract float CalulateArea();
}

public class Rectangle : Shape {
    public float width;
    public float height;

    public override float CalulateArea() { ... }
}

public class Circle : Shape {
    public float radius;

    public override float CalulateArea() { ... }
}
```
- **차이점:** 이렇게 하면 기존 코드를 수정하지 않고 새로운 기능을 추가할 수 있음. 즉, Calculator 클래스는 수정 없이도 새로운 도형의 넓이를 계산할 수 있음.

## 사용해야 할 상황
기존 코드를 변경하지 않고도 새로운 기능을 추가하거나 기존 기능을 변경하고 싶을 때 OCP를 적용해야 함.

## 장점
- **유지보수성:** 기존 코드를 수정하지 않고도 새로운 기능을 추가할 수 있으므로 유지보수가 용이함.
- **확장성:** 새로운 기능을 추가하려면 새로운 클래스를 만들고 필요한 메서드를 구현하면 됨.
- **재사용성:** 각 클래스가 독립적으로 동작하므로 다른 시스템에서도 해당 클래스를 모듈식으로 재사용하기 쉬움.

## 요약
개방-폐쇄 원칙은 클래스가 확장에 대해서는 개방적이고, 수정에 대해서는 폐쇄적이어야 한다는 설계 원칙.  
이 원칙을 따르면 코드의 유지보수성, 확장성, 재사용성이 향상됨.
