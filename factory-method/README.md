#팩토리 메서드 패턴

---

## 1. 추상화
> 팩토리 메서트는 추상화 기법을 사용하여 패턴을 확장

#### 1.1 추상개념
> 추상은 사전적 의미로 중요한 부분만 분리하여 이해하기 쉽게 만드는 작업  
> 객체에 추상적 개념을 적용하는 이유는 객체의 동작을 보다 쉽게 파악하기 위해서

---

## 2. 패턴 확장
> 추상황를 통해 팩토리 패턴을 확장, 중요한 부분만 분리하여 추상 클래스의 골격을 형성

#### 2.1 팩토리
> 팩토리 패턴은 객체지향을 지원하는 현대적 프로그래밍에서 가장 폭넓게 사용되는 패턴중 하나
> 팩토리 패턴에서는 객체 생성 요청을 별도의 클래스로 분리

#### 2.2 추상화
> 팩토리 패턴에 추상화를 결합하고 패턴을 확장해 구현  
> 추상화를 적용하면 팩토리 패턴은 팩토리 메서드 패턴과 추상 팩토리 패턴 2가리 형태로 구현
> 추상화는 선언과 구현이 자연스럽게 분리 추상화로 분리된 클래스 사이에는 의존성 발생
```java
//팩토리 추상화
public abstract class Factory {
    public final Product create() {
        return this.createProduct();
    }

    /*
     * 추상 메서드 선언
     * */
    abstract Product createProduct();
}
```
#### 2.3 인터페이스
> 인터페이스는 클래스를 설계하는 방법을 규정하는 약속  
> 인터페이스를 적용하면 반드시 인터페이스에 선언된 정의에 따라 클래스에 구현  
> 추상 클래스는 구체화되지 않은 추상 메서드를 선언 인터페이스와 유사  
> 추상 메서드는 하위 클래스에 메서드 구현을 강제화함으로써 실제적인 동작 처리를 위임
```java
//추상 메서드 선언
abstract Product createProduct();
```

#### 2.4 템플릿 메서드 패턴
> 팩토리 메서드는 실제 생성되는 알고리즘을 하위 메서드로 위임, 실제 구현을 위임한다는 측면에서 팩토리 메서드 패턴과 유사  
> 추상화를 사용하면 아직 실제 내용이 구현되지 않은 상태에서도 미리 메서드를 호출하여 사용
```java
public final Product create() {
        // return new LgProduct();
        // 하위 클래스로 위임 
        return this.createProduct();
    }
```

---

## 3. 상위 클래스
> 팩토리 메서드는 추상화를 이용해 팩토리 패턴을 재구성, 추상 클래스로 변경되면 클래스는 강제적으로 상위 클래스와 하위 클래스로 분리

#### 3.1 분리
> 추상화는 클래스의 골격 구조를 변경, 일반 클래스가 추상화로 변경되면, 클래스는 추상클래스와 구현 클래스로 분리  
> 추상화로 선언된 클래스는 일반적인 클래스 선언보다 객체의 결합 관계를 더 느슨한 관계로 변경

#### 3.2 공통된 기능
> 추상 클래스도 메서드를 구현해 하위 클래스에서 필요한 기능을 전달  
> 하위 클래스에서 사용 되는 공통된 메서드 위주로 추상 클래스 안에 구현

#### 3.3 개념적 정의
> 분리된 객체의 추상  클래스가 가진 특징은 인터페이스와 같은 개념적 메서드 선언이 가능하다. 이를 추상 메서드라 한다.
```java
//추상 메서드 선언
abstract Product createProduct();
```
#### 3.4 템플릿
> 팩토리 메서드와 템플릿 메서드의 공통점은 템플릿 구성  
> 상위 클래스에서는 구조의 모습만 정의하며 실제 모습은 하위 클래스로 위임  
> 추상화 기법은 템플릿 설계 시 요약과 세부 정보를 분리하는 데 유용

#### 3.5 계층구조
> 객체지향의 추상화는 일반 클래스를 개념적 클래스와 구현 클래스로 분리  
> 개념적 클래스를 추상 클래스, 구현 클래스를 일반 클래스라고 한다.  
> 상위 클래스에서는 문제 해결을 위한 공통 부분과 개념을 정의, 상속 시 필요한 공통 기능 및 인터페이스와 유사한 개념적 선언들로 구성  
> 즉, 상위 클래스는 구조화된 뼈대를 형성, 하위 클래스는 상위 클래스에서 선언한 뼈대를 바탕으로 실제 구현부를 작성

---

## 4. 하위 클래스
> 팩토리 메서드는 `추상 클래스 + 구현 클래스'로 분리

#### 4.1 상속
> 실제 객체를 만들기 위해서는 추상 클래스를 상속받아 구현 클래스를 만들어야 한다.

#### 4.2  메서드 구현
> 팩토리 메서드 패턴은 객체를 생성을 메서드 호출로 반환 이를 활용하는 상위 추상클래스는 보다 느슨한 코드를 작성  
> 팩토리 메서드 패턴은 객체를 생성하는 뼈대를 형성할 때 자주 응용
```java
// 팩토리 메서드 구현 부분
public class ProductFactory extends Factory {
    //추상 메서드 오버라이딩
    @Override
    Product createProduct() {
        return new LgProduct();
    }
}
```
#### 4.3 객체를 생성하는 객체
> 생성 패턴의 특징은 생성을 담당하는 객체가 요청된 객체를 생성한다는 것

#### 4.4 다형성
> 객체지향의 다형성은 구현 객체를 규격에 맞게 다양한 형태로 구현할 수 있는 것을 의미  
> 팩토리 메서드는 추상화를 통해 하위 클래스에 다형성을 부여

#### 4.5 개방-폐쇄 원픽
> 개방-폐쇄 원칙은 객체지향의 설계 원칙 중 하나, 바뀌지 않는 공통된 부분을 분리하여 관리  
> 팩토리 패턴은 객체 생성을 다른 클래스로 캡슐화 처리  
> 팩토리 메서드는 추상화를 통해 객체 생성을 유연하게 분리

#### 4.6 의존성
> 생성 패턴은 객체의 생성 과정을 외부에 공개하지 않기 위해 사용  
> 객체 생성 과젱에서 강한 의존 관계를 느슨한 관계로 처리, 의존성을 줄이기 위해서

#### 4.7 캡슐화와 관리
> 팩토리 메서드는 팩토리 패턴과 달리 캡슐화된 객체를 다시 하위 클래스로 분리  
> 분리된 클래스는 상속을 통해 실체 객체 생성 처리가 위임

---

## 5. 매개변수
> 객체 생성을 매개변수화하여 선택적으로 생성

#### 5.1 재위임
#### 5.2 다형성을 이용한 클래스 선택
> 매개변수를 이용해 다양한 객체를 선택해 생성
```java
public class SamsungProduct implements Product {

    @Override
    public String name() {
        return "Samsung Always laptop";
    }
}
```
#### 5.3 매개변수 팩토리
> 매개변수값에 의해 선택적으로 생성
> 생성 패턴은 분산된 객체의 생성 처리가 한 곳에 집중되도록 개선  
> 수정이 필요할 경우 하위 클래스만 변경하면 되므로 유지 보수가 쉽다.
```java
public class ProductFactory extends Factory {
    @Override
    public Product createProduct(String model) {
        if (model.equals("LG")) {
            return new LgProduct();
        }
        if (model.equals("SAMSUNG")) {
            return new SamsungProduct();
        }
        throw new RuntimeException("잘못된 모델명 입니다.");
    }
}
```
#### 5.4 오류처리
> 매개변수 값과 일치하지 않는 조건발생 오류를 방지하기 위해 생성 패턴에서 객체를 생성할 때 예상되는 오류들을 체크하는 코드를 삽입
```java
 public Product createProduct(String model) {
        if (model.equals("LG")) {
            return new LgProduct();
        }
        if (model.equals("SAMSUNG")) {
            return new SamsungProduct();
        }
        // 예상되는 오류 처리
        throw new RuntimeException("잘못된 모델명 입니다.");
    }
```