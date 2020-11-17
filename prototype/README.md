#프로토타입 패턴
> 객체를 생성하는 방법 new 키워드를 사용해서 생성 또는 기존에 생서된 객체를 복제하여 생성하는 것  
> 프로토타입 패턴은 new 키워드를 사용하지 않고 객체를 복제해 생성하는 패턴 
---

## 1.생성
> 시스템은 새로운 객체를 생성할 때 자원을 할당

#### 1.1 객체 생성
> 객체를 생성하기 위해서는 먼저 클래스 선언이 필요하며 선언된 클래스를 기반으로 객체를 생성.  
> 객체는 선언한 클래스의 인스턴스화를 통해 생성되고 메모리에 적재
> 객체지향에서 객체를 생성한다는 것은 시스템의 자원을 소모한다는 의미
>  
#### 1.2 객체의 상태값
> 캡슐화는 객체지향 개발 방법의 기본 개념, 행동과 데이터를 한 곳에 묵어서 관리  
> 프로그램에서 다수의 동일한 객체를 만드는 이유는 서로 다른 상탯값을 가진 객체가 필요하기 때문  
> 동일한 구조의 객체라도 사용 목적에 따라 서로 다른 프로퍼티값을 가질 수 있다.

#### 1.3 자원 소원

---

## 2. 복사
> 기존의 객체를 복사하는 것도 새로운 객체를 생성하는 방법 중 하나

#### 2.1 복사의 종류
> 생성된 객체는 변수에 할당 객체는 변수를 통해 접근 
1. 기존 변수를 공유하는 얕은 복사 
2. 새로운 자원을 할당받는 깊은 복사로 구분

#### 2.2 객체를 공유하는 얕은 복사
> 얕은 복사는 객체를 공유 방식으로 복사.   
> 공유 방식은 객체를 복사할 때 새로운 자원을 할당받지 않고 객체를 복사하는것  

```java
   void copy() {
        //객체를 생성합니다.
        final Hello obj = new Hello("안녕하세요");
        System.out.println(obj.getMessage());

        //객체를 복사합니다.
        Hello obj2 = obj;
        obj2.setMessage("Hello world");

        //원본 객체와 복제 객체의 메시지를 출력합니다.
        System.out.println(obj2.getMessage());
        System.out.println(obj.getMessage());
    }
```

#### 2.3 깊은 복사
> 실제 변수 영역을 복사하기 위해서는 깊은 복사를 사용해야 한다.  
> 물리적으로 할당된 변수를 다른 물리적 변수로 복사하는 것.
```java
@Test
    void copy2() {
        final Kryo kryo = new Kryo();
        kryo.register(Hello.class);

        //객체를 생성합니다.
        final Hello obj = new Hello("안녕하세요");
        System.out.println(obj.getMessage());

        //객체를 복사합니다.
        Hello obj2 = kryo.copy(obj);
        obj2.setMessage("Hello world");

        //원본 객체와 복제 객체의 메시지를 출력합니다.
        System.out.println(obj2.getMessage());
        System.out.println(obj.getMessage());
    }
```
* java 복제 라이브러리(Kryo)를 사용합니다.

---

## 3. 프로토타입 패턴
> 프로토타입 패턴은 신규 객체를 생성하지 않고 유사한 기존 객체를 복제. 
> 기존 객체를 복제하면 신규 객체를 생성하는 것보다 자원이 절약

#### 3.1 원형
> 복제 대상이 되는 우너본 객체를 원형이라고 한다.

#### 3.2 생성자 동작
> 클래스의 생성자는 객체 생성 시 자동으로 호출되는 메서드. 객체는 '인스턴스화' 라는 과정을 통해 생성

#### 3.3 복제 처리
> 새로운 객체를 생성할 때 시스템의 자원을 소모, 자원 소모란 CPU가 객체를 생성하기 위해 인스턴스화 과정의 역할을 수행한다는 것.
> 기존의 동일한 객체가 있다면 새롭게 생성하는 것보다 기존 객체를 복제하는 것이 좋은데, 이미 생성된 객체를 복제할 경우 인스턴스화 과정이 생량되기 때문

#### 3.4 자원 절약
> 객체 생성에 프로토타입 패턴을 사용하면 자원 소모를 줄일 수 있다. 프로토타입 패턴은 복잡한 과정으로 생성된 객체를 복제할 때 더 유용하다.

#### 3.5 주의 사항
> 복제는 새로운 객체를 생성하지 않습니다. 기존 객체에서 상탯값만 다른 또 다른 객체를 만드는 것
> 다수의 원형을 만들어 복제에 사용할 때는 별도로 원형 관리자를 토입하는 것도 좋은 방법

## 4. 특징
> 프로토타입은 적은 리소스로 많은 객체를 생성하는 데 유용

#### 4.1 생성 패턴

#### 4.2 대량 생산
> 객체를 효율적으로 생성하기 위해서는 중복된 인스턴스화 작업을 하지 않ㄴ는 것이 좋다.
> 프로토타입 패턴을 응용하면 적은 자원 소모로 많은 객체를 생성할 수 있다.

#### 4.3 유사 객체
> 프로토타입 패턴을 이용하면 런타임 시 새로운 객체를 복제하고 삭제할 수 있다.
> 클래스는 복수의 객체 생성과 재사용을 위해 선언됩니다. 다양한 종류의 클래스를 가지고 있는것보다는 기존에 생성한 클래스를 재사용할 수 있도록 유사하게 설계하는 것이 중요.

#### 4.4 객체 생성이 어려운 경우
> 객체를 복제해서 사용하면 실체 객체의 구체적인 형식을 몰라도 객체를 생성할 수 있다.