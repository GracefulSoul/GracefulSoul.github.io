---
title: "Leetcode Java Find if Array Can Be Sorted"
excerpt: "Leetcode - 'Find if Array Can Be Sorted' 문제 Java 풀이"
last_modified_at: 2024-11-06T18:50:00
header:
  image: /assets/images/leetcode/find-if-array-can-be-sorted.png
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
[Link](https://leetcode.com/problems/find-if-array-can-be-sorted/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean canSortArray(int[] nums) {
    int prevMax = 0;
    int currMin = 0;
    int currMax = 0;
    int prevCount = 0;
    for (int num : nums) {
      int currCount = Integer.bitCount(num);
      if (prevCount == currCount) {
        currMin = Math.min(currMin, num);
        currMax = Math.max(currMax, num);
      } else if (currMin < prevMax) {
        return false;
      } else {
        prevMax = currMax;
        currMin = currMax = num;
        prevCount = currCount;
      }
    }
    return currMin >= prevMax;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/find-if-array-can-be-sorted/submissions/1444662145/){:target="_blank"}

# 설명
1. nums를 아래 조건에 따라서 정렬을 수행할 경우, 오름차순으로 정렬이 가능한지 검증하는 문제이다.
- 연결된 두 숫자의 비트 중 1의 갯수가 동일한 경우에만 순서를 바꿀 수 있다.

2. 문제 풀이에 필요한 변수를 정의한다.
- prevMax는 이전까지의 최댓값을 저장한 변수로, 0으로 초기화한다.
- currMin과 currMax는 이전까지의 최솟값과 최댓값을 저장할 변수로, 둘 다 0으로 초기화한다.
- prevCount는 이전 숫자의 비트 중 1의 갯수를 저장한 변수로, 0으로 초기화한다.

3. nums의 각 숫자를 순차적으로 num을 넣어 아래를 수행한다.
- currCount는 num의 비트 중 1의 갯수를 저장한 변수이다.
- prevCount와 currCount가 동일한 교체가 가능한 경우, 아래를 수행한다.
  - currMin에 해당 값과 현재 값인 num 중 작은 값을 넣어준다.
  - currMax에 해당 값과 현재 값인 num 중 큰 값을 넣어준다.
- currMin이 prevMax보다 작은 오름차순이 성립되지 않는 경우, false를 주어진 문제의 결과로 반환한다.
- 위의 각 경우가 아니라면 아래를 수행한다.
  - prevMax에 currMax를 넣어 현재까지 가장 큰 값을 저장한다.
  - currMin과 currMax에 num을 넣어준다.
  - prevCount에 currCount를 넣어 현재 숫자의 비트 중 1의 갯수를 저장한다.

4. 반복이 완료되면 마지막으로 currMin이 prevMax보다 크거나 같은 오름차순 정렬이 성립 가능한지 여부를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindIfArrayCanBeSorted.java){:target="_blank"}에서 확인 가능합니다.