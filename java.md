```
{접근제한자} {유형 선언} {이름} {상속 키워드}
```

### 접근제한자

- public
- protected
- private

### 유형 선언

- class
- interface
- enum
- record

### 상속 키워드

- extends
- implements

#### 상속 키워드 사용 설명

- class 와 interface 만 상속가능

```java
class A {
  int a;
}
class B extends A {
  int b;
}
```

`class B` 는 상속 즉 extends (연장, 확장) 하므로, field variable 로 int a, int b를 가짐
