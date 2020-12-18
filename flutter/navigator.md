# Navigator

- 스택처럼 LIFO 방식으로 구현
- push 하면 해당 페이지로 이동
- pop 하면 이전 페이지로 이동
- context에는 페이지 간에 전달할 내용들 포함 가능

ex) 해당 페이지 이동

```dart
BottomButton(
            buttonTitle: 'CALCULATE',
            onTap: () {
              CalculatorBrain calc = CalculatorBrain(
                height: userHeight,
                weight: weight,
              );
              Navigator.push(
                context,
                MaterialPageRoute(
                  builder: (context) => ResultsPage(
                    bmiResult: calc.calculateBMI(),
                    resultText: calc.getResult(),
                    interpretation: calc.getInterpretation(),
                  ),
                ),
              );
            },
          ),
```

ex) 이전 페이지로 되돌아가기

```dart
BottomButton(
            onTap: () {
              Navigator.pop(context);
            },
            buttonTitle: 'RE-CALCULATE',
          ),
```
