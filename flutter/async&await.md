# Async & Await

- Flutter(dart)에서 비동기 작업 처리

## Future

- future는 어떤 작업 결과값을 나중에 받기로 약속하는 것<br/>
  -> 요청한 작업의 결과를 기다리지 않고 바로 다음 작업으로 넘어감
- async, await을 이용하면 기다렸다가 다음 작업 수행 가능

### Future 상태

1. Uncompleted: 미완료 상태, future객체를 만들어서 작업을 요청한 상태
2. Completed: 완료 상태, 요청한 작업이 완료된 상태<br/>
   2-1. data: 작업의 정상 종료<br/>
   2-2. error: 작업의 비정상 종료

### 비동기 함수 사용 방법

```dart
void performTasks() async {
  task1();
  print(task2());
  String task2Results = await task2();
  task3(task2Results);
}
```

- async와 await은 한 쌍으로 사용
- 함수명 뒤에 async를 붙이면, 해당 함수 내에서 await 키워드 사용 가능
- await이 붙은 작업은 해당 작업이 끝날 때까지 기다림

## 사용예시

```dart
void main() {
  performTasks();
}

void performTasks() async {
  task1();
  print(task2());
  String task2Results = await task2();
  task3(task2Results);
}

void task1() {
  String result = 'task 1 data';
  print('Task 1 complete');
}

Future<String> task2() async {
  Duration threeSeconds = Duration(seconds: 3);
  String result;
  await Future.delayed(threeSeconds, () {
    result = 'task 2 data';
    print('Task 2 complete');
  });

  return result;
}

void task3(String task2Data) {
  String result = 'task 3 data';
  print('Task 3 complete with $task2Data');
}

```

```
Task 1 complete
Instance of 'Future<String>'
Task 2 complete
Task 2 complete
Task 3 complete with task 2 data
```
