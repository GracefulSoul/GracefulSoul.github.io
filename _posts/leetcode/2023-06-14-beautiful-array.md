---
title: "Leetcode Java Beautiful Array"
excerpt: "Leetcode Beautiful Array Java"
last_modified_at: 2023-06-14T19:00:00
header:
  image: /assets/images/leetcode/beautiful-array.png
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
[Link](https://leetcode.com/problems/beautiful-array){:target="_blank"}

# 코드
```java
class Solution {

  public int[] beautifulArray(int n) {
    return this.dfs(new HashMap<>(), n);
  }

  private int[] dfs(Map<Integer, int[]> map, int n) {
    if (map.containsKey(n)) {
      return map.get(n);
    } else {
      int[] result = new int[n];
      if (n == 1) {
        result[0] = 1;
      } else {
        int index = 0;
        for (int num : this.dfs(map, (n + 1) / 2)) {
          result[index++] = (2 * num) - 1;
        }
        for (int num : this.dfs(map, n / 2)) {
          result[index++] = 2 * num;
        }
      }
      map.put(n, result);
      return result;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/beautiful-array/submissions/971008249/){:target="_blank"}

# 설명
1. 아래의 규칙을 만족하는 n 길이인 임의의 아름다운 배열인 nums를 만드는 문제이다.
- nums는 [1, n] 범위의 정수로 이루어진 배열이다.
- 0 <= i < j < n일때, $2 \times nums[k] = nums[i] + nums[j]$를 만족하는 i < k < j인 k가 존재하지 않는다.

2. 3번에서 정의한 dfs(Map<Integer, int[]> map, int n) 메서드를 수행한 결과를 주어진 문제의 결과로 반환한다.

3. DFS 방식으로 아름다운 배열을 만들기 위한 dfs(Map<Integer, int[]> map, int n) 메서드를 정의한다.
- map에 키가 n인 배열이 존재하면 해당 배열을 반환한다.
- 위가 아니라면 result에 n 크기의 배열을 만들어준다.
- n이 1인 경우, result의 첫 위치에 1을 넣어준다.
- n이 1이 아니면 아래를 수행한다.
  - index는 result의 위치 값을 저장할 변수로, 0으로 초기화한다.
  - n의 위치에 $\frac{n + 1}{2}$을 넣고 재귀 호출을 수행한 결과의 모든 값을 num에 넣고, result의 index번째 위치에 $(2 \times num) - 1$을 넣고 index를 증가시켜 앞 부분에 아름다운 배열이 되기 위한 조건의 값을 넣어준다.
  - n의 위치에 $\frac{n}{2}$을 넣고 재귀 호출을 수행한 결과의 모든 값을 num에 넣고, result의 index번째 위치에 $2 \times num$을 넣고 index를 증가시켜 뒷 부분에 아름다운 배열이 되기 위한 조건의 값을 넣어준다.
- map의 n에 해당하는 값에 result를 넣고 result를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/BeautifulArray.java){:target="_blank"}에서 확인 가능합니다.