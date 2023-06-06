---
title: "Leetcode Java Can Make Arithmetic Progression From Sequence"
excerpt: "Leetcode Can Make Arithmetic Progression From Sequence Java"
last_modified_at: 2023-06-06T09:30:00
header:
  image: /assets/images/leetcode/can-make-arithmetic-progression-from-sequence.png
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
[Link](https://leetcode.com/problems/can-make-arithmetic-progression-from-sequence){:target="_blank"}

# 코드
```java
class Solution {

  public boolean canMakeArithmeticProgression(int[] arr) {
    int length = arr.length;
    int min = Integer.MAX_VALUE;
    int max = Integer.MIN_VALUE;
    for (int num : arr) {
      min = Math.min(min, num);
      max = Math.max(max, num);
    }
    int diff = max - min;
    if (diff % (length - 1) != 0) {
      return false;
    }
    diff /= length - 1;
    for (int i = 0; i < length;) {
      int num = arr[i] - min;
      if (num == diff * i) {
        i++;
      } else if (num % diff != 0) {
        return false;
      } else {
        int position = num / diff;
        if (position < i || arr[position] == arr[i]) {
          return false;
        }
        int temp = arr[position];
        arr[position] = arr[i];
        arr[i] = temp;
      }
    }
    return true;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/can-make-arithmetic-progression-from-sequence/submissions/964770392/){:target="_blank"}

# 설명
1. arr의 숫자들을 정렬하여 산술 급수를 만들 수 있는지 검증하는 문제이다.
- 두 개 이상의 연속된 숫자의 차이가 동일한 경우, 산술 급수라고 한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 arr의 길이를 저장한 변수이다.
- min과 max는 arr의 최솟값과 최댓값을 넣을 변수로, arr을 반복하여 최솟값과 최댓값을 넣어준다.
- diff는 max와 min의 차이를 저장한 변수이다.

3. diff를 $length - 1$로 나눈 나머지가 0이 아닌 경우, arr의 모든 값들이 균등하게 증가할 수 없으므로 false를 주어진 문제의 결과로 반환한다.

4. diff에 $length - 1$로 나눈 값인 숫자들 간 차이를 넣어준다.

5. i가 0부터 length 미만까지 아래를 수행한다.
- num에 arr의 i번째 값과 min의 차이 값을 넣어준다.
- num이 diff와 i를 곱한 값과 같으면 점층적으로 증가하므로 i를 증가시켜준다.
- 위가 경우가 아니면서 num을 diff로 나눈 나머지가 0이 아닌 경우, 증가하는 값이 다르므로 false를 주어진 문제의 결과로 반환한다.
- 위의 경우가 아니면 아래를 수행한다.
  - position에 $\frac{num}{diff}$을 넣어준다.
  - position이 i보다 작거나 arr의 i번째 값과 position번째 값이 동일하면, 증가하는 경우가 아니므로 false를 주어진 문제의 결과로 반환한다.
  - arr의 i번째 값과 position번째 값을 바꾸어준다.

6. 반복이 정상적으로 종료되면 arr의 값들로 산술 급수를 만들 수 있으므로, true를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CanMakeArithmeticProgressionFromSequence.java){:target="_blank"}에서 확인 가능합니다.