---
title: "Leetcode Java Random Pick Index"
excerpt: "Leetcode Random Pick Index Java 풀이"
last_modified_at: 2022-02-26T14:00:00
header:
  image: /assets/images/leetcode/random-pick-index.png
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
[Link](https://leetcode.com/problems/random-pick-index/){:target="_blank"}

# 코드
```java
class Solution {

  int[] nums;
  Random random;

  public Solution(int[] nums) {
    this.nums = nums;
    this.random = new Random();
  }

  public int pick(int target) {
    int index = -1;
    int max = 1;
    for (int idx = 0; idx < nums.length; idx++) {
      if (nums[idx] == target && random.nextInt(max++) == 0) {
        index = idx;
      }
    }
    return index;
  }

}

/**
 * Your Solution object will be instantiated and called as such:
 * Solution obj = new Solution(nums);
 * int param_1 = obj.pick(target);
 */
```

# 결과
[Link](https://leetcode.com/submissions/detail/649030173/){:target="_blank"}

# 설명
1. 주어진 정수 배열 nums를 이용하여 임의의 정수를 추출하는 Solution 객체를 만드는 문제이다.
- 생성자인 Solution(int[] nums)은 Solution 객체를 초기화 하는 역할을 수행한다.
- 메서드인 pick(int target)은 target에 해당하는 값들 중 임의의 index를 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- nums는 생성자를 통해 주입된 정수 배열을 임시 보관하기 위한 배열이다.
- random은 반복된 값들 중 임의 위치를 반환하기 위한 변수이다. 

3. 생성자인 Solution(int[] nums)를 정의한다.
- 주어진 변수 nums를 전역 변수 nums에 넣어준다.
- random 전역 변수를 Random 객체로 초기화 한다.

4. 메서드인 pick(int target)을 정의한다.
- 위치 값을 넣기 위한 변수 result를 -1로, random의 임의 값을 구한기 위한 값을 max로 정의한다.
- nums의 위치를 idx로 처음부터 끝까지 반복을 수행한다.
  - nums의 idx번째 값이 target과 동일하고, random을 이용한 결과가 만족할 경우 index에 idx 값을 넣어준다.
- 반복이 종료되면 target의 임의 위치 값을 넣은 result를 주어진 문제의 결과로 반환한다.
  
# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/object/solution/random/pick/Solution.java){:target="_blank"}에서 확인 가능합니다.