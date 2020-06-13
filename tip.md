- 피보나치 구하기

```c
//피보나치 반복문
func solution(_ n:Int) -> Int {
    var head = 0, mid = 0, rear = 1

    for i in 0..<n {
        print(head)
        mid = head + rear
        head = rear
        rear = mid
    }
    return 0
}
print(solution(10))

//피보나치 재귀
func fibo(_ num: Int) -> Int {
    if num == 0 {
        return 0
    } else if num == 1 {
        return 1
    } else {
        return fibo(num - 1) + fibo(num - 2)
    }
}

func solution(_ n: Int) {
    for i in 0..<n {
        print(fibo(i))
    }
}
print(solution(10))
```

- DFS를 이용한 모든경우의 수 가져오기 중복X([1,2,3] 일때 1,,2,3,12,13,23,123

```c
let arr = [1,2,3]

var visit: [Bool] = Array(repeating: false, count: 3)
var temp: [Int] = [1,2,3]
var result: [Int] = []

func dfs(_ n: Int) {
    if n == temp.count {
        for i in 0..<visit.count {
            if visit[i] {
                result.append(arr[i])
            }
        }
        print(result.map { String($0) }.joined())
        result.removeAll()
    } else {
        visit[n] = true
        temp[n] = arr[n]
        dfs(n+1)
        visit[n] = false
        dfs(n+1)
    }
}

dfs(0) // 123, 12, 13, 1, 23, 2, 3
```

- 브루트 포스(조합 - 재귀) 사전순서X (순열과 다른점은 1,2,3과 3,2,1은 같은 수로 본다.)
ex) 1,2,3,4,5에서 3개의 숫자만 가져와서 조합해주기

```c
import Foundation

var arr: [Int] = []
var result: [Int] = []
var count = 0 //하나의 경우만 가져오기위해서 count처리 해줬음(만약 몇가지의 수가 있는지 체크하려면 없애도 됨.)

for _ in 0...8 {
    arr.append(Int(readLine()!)!)
}

var select: [Bool] = Array(repeating: false, count: arr.count)

func Prints() {
    result.removeAll()
    for i in 0..<arr.count {
        if select[i] == true {
            result.append(arr[i])
        }
    }
    if result.reduce(0, +) == 100 {
        count += 1
        result.sort()
        for j in 0..<result.count {
            print(result[j])
        }
    }
}

func DSF(_ idx: Int, _ cnt: Int) {
    if cnt == 7 {
        Prints()
    }
    
    for i in idx..<arr.count {
        if count == 1 { break }
        if select[i] == true {
            continue
        }
        select[i] = true
        DSF(i, cnt + 1)
        select[i] = false
    }
}
DSF(0,0)
```

- 브루트 포스(순열 - 재귀) 사전순서X 

```c
var arr = [1,2,3,4]
func log(_ size: Int) {
    var ar: [Int] = []
    for i in 0..<size {
        ar.append(arr[i])
    }
    print(ar.map{ String($0) }.joined())
}

func Permutation(_ n: Int, _ r: Int, _ depth: Int) {
    if r == depth {
        log(depth)
        return
    }
    
    for i in depth..<n {
        arr.swapAt(i, depth)
        Permutation(n,r,depth + 1)
        arr.swapAt(i, depth)
    }
}

print(Permutation(arr.count,3,0)) // 배열count 중에 3개의 숫자를 가지고 순열시킨다.
```
- 브루트 포스(순열 - 재귀) 사전순서O

```c
let N = 4
var sum: [Int] = []
var arr: [Int] = [1,2,3,4]

func rightRotate(_ arr: inout [Int], _ e: Int, _ s: Int) {
    let temp: Int = arr[e]
    for i in stride(from: e, to: s, by: -1) {
        arr[i] = arr[i-1]
    }
//    for i in (e..<s).reversed() { -> 감소문을 이렇게 쓰면 upperBound < lowerBound 에러남. 그래서 stride로 감소문을 작성
//        arr[i] = arr[i-1]
//    }
    arr[s] = temp
}


func leftRotate(_ arr: inout [Int], _ s: Int, _ e: Int) {
    let temp: Int = arr[e]
    for i in e..<s {
        arr[i] = arr[i+1]
    }
    arr[s] = temp
}

func permutation(_ arr: inout [Int], _ depth: Int) {
    if depth == N {
        for i in 0..<N {
            sum.append(arr[i])
        }
        print(sum.map{ String($0) }.joined())
        sum.removeAll()
        return
    }

    for i in depth..<N {
        rightRotate(&arr, i, depth)
        permutation(&arr, depth+1)
        leftRotate(&arr, i, depth)
    }
}

print(permutation(&arr, 0))
```

- Unicode

```c
var char = "A"
UnicodeScalar(char)?.value //65 -> UInt32

let num = 97
if let num = UnicodeScalar(num){
    print(num) //a
}

//문자열 Unicode가져오기
let str = "abcDEF"
for index in str.utf16 {
    print(index)// 97 98 99 68 69
}

```

- reduce

```c
//String배열의 총합 구하기 
for i in 0..<100 {
    let sum = Array(String(i)).reduce(0, { Int(String($0))! + Int(String($1))! })
    //먼저 string으로 변환 후 Array형태로 변경하고 reduce를 사용하여 $0값을 String -> Int형으로 변형하여 + 해주면 된다.
}
```

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
