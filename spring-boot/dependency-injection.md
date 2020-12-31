# Dependency Injection

- 필요한 객체를 직접 생성하는 것이 아닌 외부로부터 객체를 받아서 사용
- 객체간의 결합도를 줄이고 코드의 재활용성을 높이는 방법

## 장점

- Unit Test가 용의해짐
- 코드의 재활용성 증가
- 객체 간의 의존성을 줄일 수 있음
- 유연한 코드 작성 가능

## 적용 방법

### 생성자 주입

```java
@Component
public class SampleController {
    private SampleRepository sampleRepository;

    @Autowired
    public SampleController(SampleRepository sampleRepository) {
        this.sampleRepository = sampleRepository;
    }
}
```

- 생성자에 @Autowired 애노테이션을 이용해 의존성 주입
- Spring 4.3 이후로는 생성자가 하나이고, 주입받을 객체가 Bean으로 등록 되어있다면 애노테이션 생략 가능

### 필드 주입

```java
@Component
public class SampleController {
    @Autowired
    private SampleRepository sampleRepository;
}
```

- 필드에 @Autowired 애노테이션을 붙여서 의존성 주입

### Setter 주입

```java
@Component
public class SampleController {
    private SampleRepository sampleRepository;

    @Autowired
    public void setSampleRepository(SampleRepository sampleRepository) {
        this.sampleRepository = sampleRepository;
    }
}
```

- Setter메소드에 애노테이션을 붙여서 주입

### 권장 방법

- 가장 권장하는 방법은 생성자 주입<br/>
  -> 필수적으로 사용해야 하는 의존성 없이는 인스턴스를 생성 못하도록 강제 가능
- A가 B를 참조하고, B가 A를 참조하는 순환 참조의 경우, 다른 주입방법도 사용 가능<br/>
  -> 되도록 순환 참조를 피하는게 좋다

## 적용 예시

적용 전

```java
class Programmer {
    private Coffee coffee;

    public Programmer() {
    	this.coffee = new Coffee();
    }

    public startProgramming() {
    	this.coffee.drink();
        ...
    }
}
```

- Programmer는 Coffee에 의존성을 가짐
- 재활용성이 떨어짐
- Coffee를 수정할 경우, Programmer도 같이 수정을 해줘야 함

적용 후

```java
class Programmer {
    private Coffee coffee;

    public Programmer(Coffee coffee) {
    	this.coffee = coffee;
    }

    public startProgramming() {
    	this.coffee.drink();
        ...
    }
}
```

- 클래스를 직접 생성이 아닌, 주입해줌으로써 유연한 코드 작성 간으
- Coffee를 수정해도, Programmer는 수정하지 않아도 됨
