# Algorithm

###### 4. Median of Two Sorted Arrays (배열 중간값 찾기)

```c
func findMedianSortedArrays(_ nums1: [Int], _ nums2: [Int]) -> Double {
    let num3 = (nums1 + nums2).sorted()

    if num3.count % 2 == 0 {
        let middleValue = num3[num3.count / 2]
        let prevMiddleValue = num3[(num3.count / 2) - 1]
        return (Double(middleValue) + Double(prevMiddleValue)) / 2.0
    } else {
        return Double(num3[num3.count / 2])
    }
}
```

###### 58. Length of Last Word (단어 갯수 세기)

```c
func lengthOfLastWord(_ s: String) -> Int {
    if s == "" { return 0 }
    let words = s.split(separator: " ") // " "을 기준으로 단어배열생성됨
    return words.last?.count ?? 0
}
```

###### 53. Maximum Subarray (가장 큰 배열 합)

```c
func maxSubArray(_ nums: [Int]) -> Int {
    if nums.count == 0 {
        return 0
    } else if nums.count == 1 {
        return nums[0]
    } else {
        var m = 0
        var result = Int.min
        print(result)
        for i in 0..<nums.count {
            m = max(nums[i], nums[i] + m)
            
            result = max(result, m)
            print("i: \(i)  nums[]: \(nums[i])  nums+m: \(nums[i] + m) result: \(result)")
        }
        return result
    }
}
```

###### 27. Remove Element
 
```c
func removeElement(_ nums: inout [Int], _ val: Int) -> Int {
    _ = nums.map {_ in
        if let index = nums.firstIndex(of: val) {
            nums.remove(at: index)
        }
    }
    return nums.count
}
```
 
###### 3. Longest Substring Without Repeating Characters (서로 다른 문자의 최대 길이 수) 

```c
func lengthOfLongestSubstring(_ s: String) -> Int {                                                                 
    if s.count == 0 {
        return 0
    } else if s.count == 1 {
      return 1
    }
    
    var maxLength = 0
    var temp = [Character]()
    let charArray = Array(s)
    temp.append(charArray[0])
    
    for i in 1...charArray.count-1 {
        if let index = temp.firstIndex(of: charArray[i]) {
            temp.removeFirst(index+1)
        }
        temp.append(charArray[i])
        maxLength = max(maxLength, temp.count)
    }
    return maxLength
}
 ```

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

###### 88. 배열 합치고 정렬하기

```swift 
func merge(_ nums1: inout [Int], _ m: Int, _ nums2: [Int], _ n: Int) {
    nums1.removeSubrange(m...) //해당인덱스부터 remove시켜준다.
    nums1 += nums2
    
    for i in 0..<nums1.count {
        for j in 0..<nums1.count {
            if nums1[i] < nums1[j] {
                let temp = nums1[i]
                nums1[i] = nums1[j]
                nums1[j] = temp
            }
        }
    }
}
var aa = [1,2,3,0,0,0]
merge(&aa, 3, [2,5,6], 3)
```

###### 136. 중복값 제거하고 남은 숫자 가져오기
```swift 
func singleNumber(_ nums: [Int]) -> Int {
//    이것도 되지만 타임제한에 걸림
//    var intArr: [Int] = []
//
//    for num in nums {
//        if intArr.contains(num) {
//            let index = intArr.firstIndex(of: num)
//            intArr.remove(at: index!)
//        } else {
//           intArr.append(num)
//        }
//    }
//    return intArr[0]
    
    var store = Set<Int>()  //Set!
    for num in nums {
        if store.contains(num) {
            store.remove(num)
        } else {
            store.insert(num)
        }
    }
    return store.first!
}

print(singleNumber([4,1,2,1,2]))
```

###### 169. 배열안에서 가장많이 중복되는 인자값 가져오기
```swift 
 func majorityElement(_ nums: [Int]) -> Int {
    var dict: [Int: Int] = [:]
    
    for (i, num) in nums.enumerated() {
        if i == 0 {
            dict.updateValue(0, forKey: num)
        } else {
            let dic = dict.filter{ $0.key == num }
            if let key = dic.first?.key {
                let value = dict[key]! + 1
                dict.updateValue(value, forKey: key)
            } else {
                dict.updateValue(0, forKey: num)
            }
        }
    }
    return dict.filter{ $0.value == dict.values.max()}.keys.first!
}

print(majorityElement([2,1,1,2,2]))

```

###### 167. 배열의 합이 target일때 해당 index구하기 (index는 1부터 시작)
```swift 
func twoSum(_ numbers: [Int], _ target: Int) -> [Int] {
    var result: [Int] = []
    
    for i in 0..<numbers.count {
        for j in i+1..<numbers.count {
            if numbers[i] + numbers[j] == target {
                result.append(i+1)
                result.append(j+1)
            }
        }
    }
    return result
}

print(twoSum([2,3,4], 6))
```

###### 189. Rotate Array (배열을 정해진 수만큼 회전시키기)

```swift
func rotate(_ nums: inout [Int], _ k: Int) {
    for _ in 0..<k {
        nums.insert(nums.last!, at: 0) // 배열의 마지막값을 맨 앞에 추가 시켜주고
        nums.removeLast() // 마지막값을 삭제한다.
    }
}
```

###### 344. Reverse String

```swift
func reverseString(_ s: inout [Character]) {
    var i = 0
    var j = s.count - 1
    //1 i=0 j=4 result = ["o","e","l","l","h"]
    //2 i=1 j=3 result = ["o","l","l","o","h"]
    //3 i=2 j=2 끝
    while (j > i) {
        s.swapAt(i, j)
        
        i += 1
        j -= 1
    }
}
```

