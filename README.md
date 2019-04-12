# Algorithm

###### string값 string배열로 변환하기 
```swift
let strs = s.map{ String($0) }
```

###### Int형 변수 배열에 있는 값끼리 더해서 주어진 정수의 숫자와 같을때 해당 index를 구하라

```swift
nums = [2, 7, 11, 15], target = 9  --> return [0, 1]
var result: [Int] = []
for i in 0..<nums.count {
    for j in i+1..<nums.count {
        if target == nums[i] + nums[j] {
            result.append(i)
            result.append(j)
            return result
        }
    }
}
return result
```

###### 문자열 안에 문자열로 시작되는 index가져오기
```swift
let string = "Hello Swift"
if let range = string.range (of: "Swift") {
    let 시작점 = string[string.startIndex..<range.lowerBound].count
//    let location : Int = string.distance(from: string.startIndex, to: range.lowerBound)
//    print(location) //6
}
```

###### 정렬된 배열에 target이 있으면 index반환, 없으면 정렬시켜야 하는 자리의 index반환 
```swift
func searchInsert(_ nums: [Int], _ target: Int) -> Int {
    var result = 0
    for (i, num) in nums.enumerated() {
        if num == target {
            result = i
            break
        } else if num > target {
            result = i
            break
        } else {
            result = nums.count
            continue
        }
    }
    return result
}
```

###### 7. Int 숫자를 Reverse시키기
```swift
func reverse(_ x: Int) -> Int {    
    var value = x
    var resultValue = 0
    var plus: Bool = true
    
    if value > 0 {
        plus = true
    } else {
        value = value * -1
        plus = false
    }
    let str = String(String(value).reversed())
    if plus {
        resultValue = Int(str)!
    } else {
        resultValue = -Int(str)!
    }
    let val = Int(pow(Double(2),Double(31)))   // Int형의 범위를 벗어나면 0으로 리턴해주기 위해서 사용
    if resultValue > val-1 || resultValue < -val {
        return 0
    }
    return resultValue
}

reverse(1534236469)
```
###### 53. 배열안에 연속적으로 더했을때 가장 큰 값을 리턴하라.
```swift
func maxSubArray(_ nums: [Int]) -> Int {
    guard nums.count != 0 else{
        return 0
    }
    
    guard nums.count != 1 else{
        return nums[0]
    }
    
    var largestSum = nums[0]
    var sum = nums[0]
    
    for i in 1..<nums.count{
        sum = max(sum + nums[i], nums[i]) //max(a, b)를 비교하여 더 큰값을 반환한다.
        if sum > largestSum {
            largestSum = sum
        }
    }
    
    return largestSum
}

maxSubArray([-2,1,-3,4,-1,2,1,-5,4]) //6
```

###### 69. Sqrt (x의 제곱근을 구하라)
```swift 
func mySqrt(_ x: Int) -> Int {
    let result = Int(sqrt(Double(x)))   // swift4버전부터 사용할 수 있는 sqrt함수를 사용함
    return result
}
print(mySqrt(8))
```
