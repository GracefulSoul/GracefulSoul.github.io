---
title: "Leetcode Java Count Triplets That Can Form Two Arrays of Equal XOR"
excerpt: "Leetcode Count Triplets That Can Form Two Arrays of Equal XOR Java"
last_modified_at: 2024-05-29T18:40:00
header:
  image: /assets/images/leetcode/count-triplets-that-can-form-two-arrays-of-equal-xor.png
categories:
  - Leetcode
tags:
  - Programming
  - Leetcode
  - Java

toc: true
toc_ads: true
toc_sticky: true
use_math: true
---
# 문제
[Link](https://leetcode.com/problems/count-triplets-that-can-form-two-arrays-of-equal-xor/){:target="_blank"}

# 코드
```java
class Solution {

  public int countTriplets(int[] arr) {
    int result = 0;
    int length = arr.length;
    for (int i = 0; i < length; i++) {
      int temp = arr[i];
      for (int j = i + 1; j < length; j++) {
        temp ^= arr[j];
        if (temp == 0) {
          result += (j - i);
        }
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/count-triplets-that-can-form-two-arrays-of-equal-xor/submissions/1273151764/){:target="_blank"}

# 설명
1. 정수 배열인 arr을 이용하여 아래의 조건을 만족하는 삼중항(i, j, k)의 수를 반환하는 문제이다.
- $0 <= i < j <= k < arr.length$를 만족한다.
- a와 b를 아래와 같이 정의한다.
  - $a = arr[i] ^ arr[i + 1] ^ ... ^ arr[j - 1]$
  - $b = arr[j] ^ arr[j + 1] ^ ... ^ arr[k]$
  - a == b 를 만족하며, "^" 문자는 XOR 비트 연산을 의미한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 삼중항의 갯수를 저장할 변수로, 0으로 초기화한다.
- length는 arr의 길이를 저장한 변수이다.

3. 0부터 length 미만까지 i를 증가시키며 아래를 반복한다.
- temp에 arr[i]의 값을 넣고, $i + 1$부터 length 미만까지 j를 증가시키면서 아래를 반복한다.
  - temp에 temp와 arr[j]의 값을 XOR 비트 연산을 수행한 값을 넣어준다.
  - temp가 0인 경우, result에 $j - i$를 더해준다.

4. 반복이 완료되면 삼중항의 갯수가 저장된 result를 주어진 문제의 결과로 반환한다.

# 해설
- 1번 설명을 기반으로 a와 b가 동일한 값일 때, 아래를 만족한다.
  - $a = b$ 의 양 변에 b를 XOR 비트 연산을 수행한다.
  - $a ^ b = b ^ b$ 이므로, 우변은 0이 되어 $a ^ b = 0$를 만족한다.
  - 마지막으로, $a ^ b = arr[i] ^ arr[i + 1] ^ ... ^ arr[j - 1] ^ arr[j] ^ arr[j + 1] ^ ... ^ arr[k] = 0$을 만족한다.
- 위를 기반으로 두 값인 i와 k에 대해서 XOR 비트 연산이 0이 되는 경우, j를 $i + 1$부터 k까지 임의 위치시키는 경우의 수인 $j - 1$개의 경우의 수가 삼중항의 갯수가 된다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CountTripletsThatCanFormTwoArraysOfEqualXOR.java){:target="_blank"}에서 확인 가능합니다.