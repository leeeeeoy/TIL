# Stream

- 데이터나 이벤트가 들어오는 통로
- 데이터의 추가나 변경이 일어나면 이를 관찰하는 곳에서 처리

## Stream & Future

- 둘 다 비동기 프로그래밍을 처리하는데 사용
- Future는 즉시 완료되지 않는 계산<br/>
  -> 결과가 준비되면 Future에 알려줌
- Stream은 일련의 비동기 이벤트<br/>
  -> 요청 시 다음 이벤트를 받는 대신 Stream이 준비되면 이벤트가 있음을 알려줌
