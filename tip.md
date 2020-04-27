- 소수점 표현하기

```c
ceil()
//소수점 이하를 모두 버리고 정수부에 +1 을 해줍니다.

floor()
//소수점 이하를 모두 버립니다.

round()
//소수점 이하를 반올림합니다. 0.5 이상은 1로 올리고 미만은 버립니다.

String(format: "%.3f",  40.0) // 40.000
//특정 소수점 자리까지 나타내기

//특정 소수점 자리에서 반올림을 하고나서 3자리로 표현하는 방법
let input = 10.52834213
let roundedNum = round(input * 1000) / 1000
print("\(String(format: "%.3f",  roundedNum))%")
```
