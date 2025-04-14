---
title: "Leetcode Java Count Good Triplets"
excerpt: "Leetcode - 'Count Good Triplets' 문제 Java 풀이"
last_modified_at: 2025-04-14T18:20:00
header:
  image: /assets/images/leetcode/count-good-triplets.png
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
[Link](https://leetcode.com/problems/count-good-triplets/){:target="_blank"}

# 코드
```java
class Solution {

  public int countGoodTriplets(int[] arr, int a, int b, int c) {
    int length = arr.length;
    int result = 0;
    for (int i = 0; i < length - 2; i++) {
      for (int j = i + 1; j < length - 1; j++) {
        if (Math.abs(arr[i] - arr[j]) <= a) {
          for (int k = j + 1; k < length; k++) {
            if (Math.abs(arr[j] - arr[k]) <= b && Math.abs(arr[i] - arr[k]) <= c) {
              result++;
            }
          }
        }
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/count-good-triplets/submissions/1606426608/){:target="_blank"}

# 설명
1. 정수가 들어있는 arr을 이용하여 아래 조건을 만족하는 값들의 조합 수를 반환하는 문제이다.
- 0 <= i < j < k < arr.length 를 만족할 때, 아래 세 조건을 만족한다.
  - $|arr[i] - arr[j]| <= a$
  - $|arr[j] - arr[k]| <= b$
  - $|arr[i] - arr[k]| <= c$

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 arr의 길이를 저장한 변수이다.
- result는 조합 수를 저장하기 위한 변수로, 0으로 초기화한다.

3. 0부터 $length - 2$까지 i를 증가시키며, $i + 1$부터 $length - 1$까지 j를 증가시키며 아래를 반복한다.
- 첫 조건인 $|arr[i] - arr[j]| <= a$ 조건을 만족하는 경우, 아래의 수행을 계속 진행한다.
  - $j + 1$부터 length 미만까지 k를 증가시키며 $|arr[j] - arr[k]| <= b$ 조건과 $|arr[i] - arr[k]| <= c$ 조건을 만족하는 경우, result를 증가시켜준다.

4. 반복이 완료되어 계산된 조합의 수인 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CountGoodTriplets.java){:target="_blank"}에서 확인 가능합니다.