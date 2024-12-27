## Default keywords

### access_modifiers 접근제한자

- public
- protected
- private

### type 유형

- class
- interface
- enum
- record

### inherit_keywords 상속 키워드

- extends
- implements

## Object

```
`access_modifiers` `type` `name` `inherit_keywords`
```

#### 상속 키워드 사용 설명

- class 와 interface 만 상속가능

##### class

```java
class A {
  int a;
}
class B extends A {
  int b;
}
```

`class B` 는 상속 즉 extends (연장, 확장) 하므로, field variable 로 int a, int b를 가짐

##### interface

- 인터페이스는 메소드 목업 제작용도

```java
interface C {
  int methodC();
}
interface D extends C {
  int methodD();
}
```

실 사용시 포함 함수 결과

```java
interface D {
  int methodC(); // extends
  int methodD(); // extends
}
```

여러개 상속 가능

```java
interface C {
  int methodC();
}
interface E {
  int methodE();
}
interface D extends C, E {
  int methodD();
}
```

여러개 상속

실 사용시 포함 함수 결과

```java
interface D extends C, E {
  int methodD();

  int methodC(); // extends
  int methodE(); // extends
```

##### class from interface

interface implements (이행, 구현, 시행)

```java
interface A {
  int methodA();
}
class B implements A {
  int fieldVariableB;
  int methodA() {}; // interface 함수를 구현해야함
}
```

```java
interface A {
  int methodA();
}
interface C {
  int methodC();
}
class B implements A, C {
  int fieldVariableB;
  int methodA() {}; // interface 함수를 구현해야함
  int methodC() {}; // interface 함수를 구현해야함
}
```

여러개 상속 가능

##### class from class and interface

class 와 interface 상속

```java
interface A {
  int methodA();
}
interface B {
  int methodB();
}
class C {
  int fieldVariableC;
}
class D {
  int fieldVariableD;
}
class E extends C, D implements A, B {
  int fieldVariableE;
  int methodE() {};

  int methodA() {}; // interface implemtns 시 함수를 구현해야함
  int methodB() {}; // interface implemtns 시 함수를 구현해야함
}
```

결과적으로 class E 에서 사용 가능한것

```java
class E {
  int fieldVariableE;
  int methodE() {};

  int fieldVariableC; // extends from class C
  int fieldVariableD; // extends from class D

  int methodA() {}; // interface implemtns 시 함수를 구현해야함
  int methodB() {}; // interface implemtns 시 함수를 구현해야함
}
```

## field 선언

```java
public class hello {
  `access_modifiers` `(static)` `type` `name`
}
```

### Pattern

#### Singleton

##### Default Singleton pattern

```java
public class Single {
  private static Single singleton = new Single();
  private Single() {};
  static Single getInstance() {
    return singleton;
  }
}
```

##### LazyHolder pattern

```java
public class Single {
  private Single() {};
  public static Single getInstance() {
    return LazyHolder.INSTANCE;
  }
  private static class LazyHolder {
    private static final Singleton INSTANCE = new Singleton();
  }
}
```

- Thread safe 를 보장함 class 가 중복 실행안됨

#### Builder Pattern

```java

```

#### Getter Setter

```java

```
