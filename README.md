# Algorithm

###### Dictionaries and Hashmaps
- sherlockAndAnagrams 시간복잡도에서 계산이 안되네.........ㅠㅠㅠㅠㅠㅠㅠㅠㅠ 여기서 더 좋은방법이 뭘까....
```c
func sherlockAndAnagrams(s: String) -> Int {
    let arr = Array(s)
    var count = 0
    var index = 0
    var targets: [String] = []
    while index < arr.count - 1 {
        for i in 0..<arr.count - index {
            let pivot = String(arr[i..<i+index+1].sorted())
            for target in targets {
                if target == pivot {
                    count += 1
                }
            }
            targets.append(pivot)
        }
        index += 1
    }
    return count
    
   //let arr = Array(s)
   //var count = 0
   //var index = 1

   //while index < arr.count  {
   //    for i in 0..<arr.count-index {
   //        let pivot = arr[i..<i+index]
   //        print(pivot)
   //        for j in i+1..<arr.count - (index - 1) {
   //            let target = arr[j..<j+index]
   //            print(target)
   //            if pivot.sorted() == target.sorted() {
   //                count += 1
   //            }
   //        }
   //    }
   //    index += 1
  // }
  // return count
//}
print(sherlockAndAnagrams(s: "kkkk"))
```

###### String Manipulation

- 해당 문자열에서 char 갯수가 같은거만 'YES' 아니면 'NO', 한가지 단어만 -1 한번마 가능함
- Sherlock and the Valid String

```c
func valid(s: String) -> String {
    let arr = s.map{ String($0) }
    
    let dic = arr.reduce([:], { (res, current) -> [String: Int] in
        var res = res
        res[current] = (res[current] ?? 0) + 1
        return res
    })
    
    let resultDic = dic.values.reduce([:], { (res, current) -> [Int: Int] in
        var res = res
        res[current] = (res[current] ?? 0) + 1
        return res
    })
    print(resultDic) //여기서부터 -1 해주는거때문에 조건이 지저분해짐..
    if resultDic.values.count >= 3 { //갯수가 다른 문자가 3개 이상일때 무조건 NO
        return "NO"
    } else if resultDic.values.count == 1 { //모든 문자의 갯수가 같을때 무조건 YES
        return "YES"
    } else {  // [key: value, key: value] 이경우만
        let min = resultDic.values.min()! 
        let dis = resultDic.keys.reduce(0) { abs($0 - $1) } 
        if min == 1 && dis == 1 {
            return "YES"
        } else {
            if resultDic[1] == 1 {
                return "YES"
            } else {
                return "NO"
            }
        }
    }
}
print(valid(s: "aabbccddeefghi"))
```

- 두개의 문자열에서 anagrams 만들때 불필요한 문자 count 구하기
* anagrams: 앞뒤로 똑같이 해도 두 단어가 같은것

```c
func anagram(a: String, b: String) -> Int {
    var dic: [String: Int] = [:]
    _ = a.map{ String($0) }.map { str in
        
        dic[str] = (dic[str] ?? 0) + 1
    }
    print(dic)
    
    _ = b.map{ String($0) }.map { str in
        dic[str] = (dic[str] ?? 0) - 1
    }
    print(dic)
    return abs(dic.values.reduce(0, +))
}
print(anagram(a: "fcrxzwscanmligyxyvym", b: "jxwtrhvujlmrpdoqbisbwhmgpmeoke"))
```

###### Array

- que배열안의 문자열이 str에 몇개나 있는지 확인하는문제
```c
func matching(_ str: [String], _ que: [String]) -> [Int] {

    let arr = que.compactMap { str in //flatMap은 삭제되었다. compactMap을 사용
        str.filter { $0 == str }.count
    }
    return arr
}

print(matching(["aba", "baba", "aba", "xzxb"], ["aba", "xzxb", "ab"]))
```


###### Warm-up

```c
func rotLeftTest(_ a: [Int], _ d: Int) -> [Int] {
    let num = d % a.count
    var arr = a.dropFirst(num)
    arr.append(contentsOf: a.dropLast(a.count - num ))

    return Array(arr)
    
    //runtime error
    // var arr = a
    // let num = d % a.count
    
    // for _ in 0..<num { //이 for문이 runtime error를 방출시킨다.
    //     arr.append(arr[0])
    //     arr.remove(at: 0)
    // }

    // return arr
}

print(rotLeftTest([1,2,3,4,5], 53))
```

```c
func repeated(_ s: String, _ n: Int) -> Int {
    let str = s.map { String($0) }
    //let count1 = str.filter { $0 == str[0] }.count
    let count1 = str.filter { $0 == "a" }.count//주어진 문자열의 첫번째를 찾는게 아니라 "a" 를 찾는 문제였음.
    let firstSum = (n / str.count) * count1
    
    let count2 = n % str.count
    let twoSum = str[0..<count2].filter { $0 == "a" }.count
    
    return firstSum + twoSum
}
print(repeated("gfcaaaecbg", 547602))
```

```c
func sock(n: Int, ar: [Int]) -> Int {
    let set = Set<Int>(ar)
    var result = 0
    for s in set {
        result += ar.filter { $0 == s }.count / 2
    }

//run time error(reduce를 두번써서)
    // let count = ar.reduce([:], { (res, current) -> [Int: Int] in
    //     var res = res
    //     res[current, default: 0] += 1
    //     return res
    //     }).values.reduce(0, { (result, element) -> Int in
    //         return result + (element/2)
    //     })
    
    return result
}

print(sock(n: 9, ar: [10, 20, 20, 10, 10, 30, 50, 10, 20]))
```

```c
func counting(n: Int, s: String) -> Int {
    var result = 0
    _ = s.map { String($0) }
        .reduce(into: 0) { (res, s) in
            res += s == "U" ? +1 : -1
            if s == "U" && res == 0 {
                result += 1
            }
    }
    return result
}

print(counting(n: 12, s: "UDDDUDUU"))
```

=======================================leetcode=======================================

###### 1207. Unique Number of Occurrences
```c
func uniqueOccurrences(_ arr: [Int]) -> Bool {
    let ee = arr.reduce([:], { (res, current) -> [Int: Int] in
    var res = res
    res[current, default: 0] += 1  // dictionary default value
    return res
    })

    return Set(Array(ee.values)).count == ee.keys.count
}
```

###### 657. Robot Return to Origin
```c
func judgeCircle(_ moves: String) -> Bool {
    var sideNum = 0
    var upDownNum = 0
    let arr = moves.map { String($0) }
    for i in 0..<arr.count {
        switch arr[i] {
        case "U":
            upDownNum += 1
        case "D":
            upDownNum -= 1
        case "L":
            sideNum += 1
        case "R":
            sideNum -= 1
        default:
            print("")
        }
    }
    return (sideNum == 0 && upDownNum == 0) ? true : false
}
```

###### 977. Squares of a Sorted Array 
```c
 func sortedSquares(_ A: [Int]) -> [Int] {
    var arr: [Int] = []

    for a in A {
        arr.append(a * a)
    }

    return arr.sorted()
}
```

###### 961. N-Repeated Element in Size 2N Array (중복값 찾기)
```c
func repeatedNTimes(_ A: [Int]) -> Int {
    var arr: [Int] = []
    for a in A {
        if arr.contains(a) {
            return a
        } else {
            arr.append(a)
        }
    }
    return 0
}
```

###### 905. Sort Array By Parity (짝수 홀수 정렬)
```c
func sortArrayByParity(_ A: [Int]) -> [Int] {
    let even = A.filter {
        return $0 % 2 == 0
    }

    let odd = A.filter {
        return $0 % 2 != 0
    }
    return even + odd
}
```

###### 804. Unique Morse Code Words (문자열 모스부호로 변경하고 )
```c
func uniqueMorseRepresentations(_ words: [String]) -> Int {
        let morseCode = [".-","-...","-.-.","-..",".","..-.","--.","....","..",".---","-.-",".-..","--","-.","---",".--.","--.-",".-.","...","-","..-","...-",".--","-..-","-.--","--.."]
        
        let result = Set<String>(words.map {
        $0.utf8.map {
            return morseCode[Int($0 - 97)]
        }.joined()
    })    
    return result.count
}
```

###### 709. To Lower Case (대문자를 소문자로 변경하기)
```c
func toLowerCase(_ str: String) -> String {
//    return str.lowercased()  //이것도 가능하지만 생략
    
    //아스키코드로 변경진행해봤음
    return str.utf8.map {
        $0 <= 90 && $0 >= 65 ? String(UnicodeScalar($0 + 32)): String(UnicodeScalar($0))  //대문자 -> 소문자
//        $0 >= 97 && $0 <= 122 ? String(UnicodeScalar($0 - 32)): String(UnicodeScalar($0))  // 소문자 -> 대문자
    }.joined()
}
```

###### 1281. Subtract the Product and Sum of Digits of an Integer (배열 곱 - 합)
```c
func subtractProductAndSum(_ n: Int) -> Int {
    let arr = String(n)
    .map { String($0) }
    
    //이거 한번에 처리하는방버 없나?..
    let mul = arr.reduce(1) {
        return Int($0) * Int($1)!
    }
    let plus = arr.reduce(0) {
        return Int($0) + Int($1)!
    }
    return mul-plus
}
```

###### 1108. Defanging an IP Address (문자열치환)
```c
func defangIPaddr(_ address: String) -> String {
    return address.replacingOccurrences(of: ".", with: "[.]")
}
```

###### 1295. Find Numbers with Even Number of Digits (index가 짝수인거 찾기)
```c
func findNumbers(_ nums: [Int]) -> Int {
    let result = nums
    .map { Array(String($0)) }   //Array(문자열마 가능함)
    .filter { $0.count % 2 == 0 }

    return result.count
}
```

###### 434. Number of Segments in a String (문자열 나눠서 갯수 구하기)
```c
func countSegments(_ s: String) -> Int {
    let arr = s.split(separator: " ")
    return arr.count
}
```

###### 414. Third Maximum Number (배열에서 세번째로 높은 수 찾기)
```c
 func thirdMax(_ nums: [Int]) -> Int {  // 배열에서 max값 1,2번째를 버리고 남은 배열의 max값을 가지고 온다.
    var arr = Set<Int>(nums)

    if arr.count < 3 {
        return arr.max()!
    } else {
        for _ in 0..<2 {
            arr.remove(arr.max()!)
        }
    }
    return arr.max()!
}
```

###### 412. Fizz Buzz
```c
func fizzBuzz(_ n: Int) -> [String] {
    let three = "Fizz"
    let five = "Buzz"
    var arr: [String] = []

    for i in 1...n {
        if i % 3 == 0 && i % 5 == 0 {
            arr.append("\(three)\(five)")
        } else if i % 3 == 0 {
            arr.append("\(three)")
        } else if i % 5 == 0 {
            arr.append("\(five)")
        } else {
            arr.append("\(i)")
        }
    }
    return arr
}
```

###### 389. Find the Difference (다른 한단어 찾기)

```c
func findTheDifference(_ s: String, _ t: String) -> Character {
    var str: Character = " "
    let s = s.map { String($0) }
    let t = t.map { String($0) }
    let sArr = s.sorted()
    let tArr = t.sorted()
    
    for i in 0..<sArr.count {
        if sArr[i] == tArr[i] {
            continue
        } else {
            str = Character(tArr[i])
            break
        }
    }    
    
    if str == " " {
        str = Character(tArr.last!)
    }
    
    return str
}
```

###### 258. Add Digits (자리수 합이 10이하가 되면 됨) map, filter, reduce를 활용하는걸 더 추천

```c
func addDigits(_ num: Int) -> Int {
    var str = num
    while str > 0 {
        str = String(str).map {
            String($0)
        }.reduce(0) {
            Int($0) + Int($1)!
        }
    
        if str < 10 { break }
    }
    return str
}
```

###### 242. Valid Anagram (anagram: 철자 순서를 바꾼 말)

```c
func isAnagram(_ s: String, _ t: String) -> Bool {
  if s == "" && t == "" { return true }
  if s.sorted() == t.sorted() {
    return true
  } else {
    return false
  }
}
```

###### 217. Contains Duplicate (중복값 있는지 체크)

```c
 func containsDuplicate(_ nums: [Int]) -> Bool {
   let setNums = Set<Int>(nums)

    if nums.count == setNums.count {
        return false
    } else {
        return true
    }
}
```

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

