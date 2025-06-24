---
title: "Leetcode Java Find All K-Distant Indices in an Array"
excerpt: "Leetcode - 'Find All K-Distant Indices in an Array' 문제 Java 풀이"
last_modified_at: 2025-06-24T19:20:00
header:
  image: /assets/images/leetcode/find-all-k-distant-indices-in-an-array.png
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
[Link](https://leetcode.com/problems/find-all-k-distant-indices-in-an-array/){:target="_blank"}

# 코드
```java
class Solution {

  public List<Integer> findKDistantIndices(int[] nums, int key, int k) {
    List<Integer> result = new ArrayList<>();
    int curr = 0;
    int length = nums.length;
    for (int i = 0; i < length; i++) {
      if (nums[i] == key) {
        int j = Math.max(curr, i - k);
        curr = Math.min(i + k, length - 1) + 1;
        while (j < curr) {
          result.add(j++);
        }
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/find-all-k-distant-indices-in-an-array/submissions/1674760787/){:target="_blank"}

# 설명
1. nums 내 key와 동일한 값을 포함한 좌우 k개의 중복되지 않은 위치 값을 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 위치 값을 저장할 변수로, ArrayList로 초기화한다.
- curr은 현재까지 탐색한 마지막 위치를 저장할 변수로, 0으로 초기화한다.
- length는 nums의 길이를 저장한 변수이다.

3. 0부터 length 미만까지 i를 증가시키며 아래를 반복한다.
- nums[i]의 값이 key와 동일한 경우, 아래를 수행한다.
  - j는 위치 값을 넣기 위한 시작 위치를 저장할 변수로, curr과 현재 위치에서 k 이전 위치인 $i - k$ 중 큰 값을 넣어준다.
  - curr은 현재 위치에서 k 이후 위치인 $i + k$와 마지막 위치인 $length - 1$ 중 작은 값에 1을 더해서 넣어준다.
  - j가 curr 미만까지 result에 curr의 값을 넣고 j를 증가시켜준다.

4. 반복이 완료되면 저장된 restul를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindAllKDistantIndicesInAnArray.java){:target="_blank"}에서 확인 가능합니다.