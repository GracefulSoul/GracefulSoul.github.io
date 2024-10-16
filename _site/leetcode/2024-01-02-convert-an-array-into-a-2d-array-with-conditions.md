---
title: "Leetcode Java Convert an Array Into a 2D Array With Conditions"
excerpt: "Leetcode Convert an Array Into a 2D Array With Conditions Java"
last_modified_at: 2024-01-02T12:50:00
header:
  image: /assets/images/leetcode/convert-an-array-into-a-2d-array-with-conditions.png
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
[Link](https://leetcode.com/problems/convert-an-array-into-a-2d-array-with-conditions){:target="_blank"}

# 코드
```java
class Solution {

  public List<List<Integer>> findMatrix(int[] nums) {
    List<List<Integer>> result = new ArrayList<>();
    int[] counts = new int[nums.length + 1];
    for (int num : nums) {
      if (result.size() <= counts[num]) {
        result.add(new ArrayList<>());
      }
      result.get(counts[num]++).add(num);
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/convert-an-array-into-a-2d-array-with-conditions/submissions/1134247762/){:target="_blank"}

# 설명
1. nums의 요소들을 아래의 규칙대로 모아 반환하는 문제이다.
- nums 안의 값들만 사용하여 중복되지 않은 정수를 모은다.
- 정수 집합의 크기는 최소화하여야 한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 정수 집합을 저장할 변수로, ArrayList로 초기화한다.
- counts는 정수를 따로 저장하기 위해 사용할 변수로, nums의 길이보다 1 큰 정수 배열로 초기화한다.

3. nums의 모든 값을 num에 넣어 아래를 반복한다.
- result의 길이보다 counts[num]의 값이 같거나 작은 경우, result에 새로운 정수 집합을 넣기 위해 ArrayList를 넣어준다.
- result에 counts[num]번째 List를 꺼내 num을 넣은 후, 반복된 값이 들어가지 않기 위해서 counts[num]을 증가시킨다.

4. 반복이 완료되면 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ConvertAnArrayIntoA2DArrayWithConditions.java){:target="_blank"}에서 확인 가능합니다.