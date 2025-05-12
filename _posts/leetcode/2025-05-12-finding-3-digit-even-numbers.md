---
title: "Leetcode Java Finding 3-Digit Even Numbers"
excerpt: "Leetcode - 'Finding 3-Digit Even Numbers' 문제 Java 풀이"
last_modified_at: 2025-05-12T18:50:00
header:
  image: /assets/images/leetcode/finding-3-digit-even-numbers.png
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
[Link](https://leetcode.com/problems/finding-3-digit-even-numbers/){:target="_blank"}

# 코드
```java
class Solution {

  public int[] findEvenNumbers(int[] digits) {
    int[] counts = new int[10];
    for (int digit : digits) {
      counts[digit]++;
    }
    List<Integer> list = new ArrayList<>();
    for (int i = 1; i < 10; i++) {
      if (0 < counts[i]) {
        counts[i]--;
        for (int j = 0; j < 10; j++) {
          if (0 < counts[j]) {
            counts[j]--;
            for (int k = 0; k < 10; k += 2) {
              if (0 < counts[k]) {
                list.add(i * 100 + j * 10 + k);
              }
            }
            counts[j]++;
          }
        }
        counts[i]++;
      }
    }
    return list.stream().mapToInt(i -> i).toArray();
  }

}
```

# 결과
[Link](https://leetcode.com/problems/finding-3-digit-even-numbers/submissions/1631775997/){:target="_blank"}

# 설명
1. [0, 9] 사이 값들로 이루어진 digits 내 숫자들을 이용하여 중복되지 않은 짝수인 세 자리 숫자를 모두 만드는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- counts는 digits 내 값들의 갯수를 계산할 변수로, 10 크기의 정수 배열로 초기화하고 digits 내 각 값들의 갯수를 넣어준다.
- list는 만들 수 있는 세 자리 숫자들을 넣을 변수로, ArrayList로 초기화한다.

3. 1부터 10 미만까지 i를 증가시키며 아래를 반복한다.
- counts[i] 값이 0보다 큰 경우, counts[i]를 감소시키고 0부터 10 미만까지 j를 증가시키며 아래를 반복한다.
  - counts[j]의 값이 0보다 큰 경우, counts[j]를 감소시키고 0부터 10 미만까지 k를 2씩 증가시키며 counts[k]의 값이 0보다 크면 list에 $i \times 100 + j \times 10 + k$의 값을 넣어준다.
  - counts[j]의 값을 다시 증가시켜 값을 복원해준다.
- counts[i]의 값을 다시 증가시켜 값을 복원해준다.

4. 완성된 list를 정수 배열로 변환하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/Finding3DigitEvenNumbers.java){:target="_blank"}에서 확인 가능합니다.