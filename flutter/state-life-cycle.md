# State Lifecycle

- 두 상태를 분리한건 성능과 관련되어 있음
- State: 사용되는 Data

## Stateless

- 생성자를 통해 객체나 값을 전달함
- 상호작용이 필요없는 Widget
- Stateful에 비해 LifeCycle이 빠름

## Stateful

### initState()

- Widget이 생성될 때 가장 처음 호출됨
- 상태를 초기화 하며, 단 한번만 호출됨
- super.initState() 을 반드시 호출해야 함

### didChangeDependencies()

- 상태 객체의 의존성이 변경되면 호출
- initState() 다음에 호출됨
- 네트워크 호출 등의 비용이 많이 드는 액션에 이용?

### build()

- 필수적으로 override 해야하는 메소드
- 화면에 표시할 Widget을 반환
- 반드시 Widget을 return 해야 함

### didUpdateWidget()

- Widget의 설정이 변경될 때 호출
- 부모 Widget이 변경되어 재 구성 하는 경우

### setState()

- Widget의 State를 갱신
- 이 메소드를 실행하면 Widget이 처음부터 다시 만들어 짐
- initState() 메소드는 호출하지 않음

### dispose()

- State객체가 Widget tree 에서 영구 제거
- 이 메소드 호출 이후에는 재사용 불가
