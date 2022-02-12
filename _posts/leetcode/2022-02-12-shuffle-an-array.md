---
title: "Leetcode Java Shuffle an Array"
excerpt: "Leetcode Shuffle an Array Java 풀이"
last_modified_at: 2022-02-12T13:00:00
header:
  image: /assets/images/leetcode/shuffle-an-array.png
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
[Link](https://leetcode.com/problems/shuffle-an-array/){:target="_blank"}

# 코드
```java
class Solution {

  private int[] nums;
  private int[] copy;
  private Random random;

  public Solution(int[] nums) {
    this.nums = nums;
    this.copy = Arrays.copyOf(nums, nums.length);
    this.random = new Random();
  }

  public int[] reset() {
    this.copy = Arrays.copyOf(nums, nums.length);
    return this.copy;
  }

  public int[] shuffle() {
    for (int idx = this.copy.length - 1; idx >= 0; idx--) {
      int num = this.random.nextInt(idx + 1);
      int temp = this.copy[num];
      this.copy[num] = this.copy[idx];
      this.copy[idx] = temp;
    }
    return this.copy;
  }

}

/**
 * Your Solution object will be instantiated and called as such:
 * Solution obj = new Solution(nums);
 * int[] param_1 = obj.reset();
 * int[] param_2 = obj.shuffle();
 */
```

# 결과
[Link](https://leetcode.com/submissions/detail/639635053/){:target="_blank"}

# 설명
1. 정수 배열 nums가 주어지면, 무작위로 섞고 초기화가 가능한 Solution 객체를 만드는 문제이다.
- 생성자인 Solution(int[] nums)는 주어진 정수 배열 nums로 Solution 객체를 초기화한다.
- 메서드인 int[] reset()은 Solution 내 배열을 재 설정하여 반환한다.
- 메서드인 int[] suffle()은 Solution 내 배열을 무작위로 섞어 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- nums는 주어진 정수 배열을 원본으로 저장하기 위한 변수이다.
- copy는 nums를 복사해서 무작위로 섞어 보관할 변수이다.
- random은 객체 내 존재하는 값을 임의 확률로 반환하기 위한 객체이다.

3. 생성자인 Solution(int[] nums)을 완성한다.
- nums에 주어진 정수 배열인 nums를 넣어준다.
- copy에 nums를 [깊은 복사](https://en.wikipedia.org/wiki/Object_copying#:~:text=Deep%20copy%20is%20a%20process,objects%20found%20in%20the%20original.&text=It%20means%20that%20any%20changes,reflect%20in%20the%20original%20object.){:target="_blank"}하여 넣어준다.
- random에 Random 객체로 초기화 시켜준다.

4. 메서드인 int[] reset()을 완성한다.
- 생성자와 동일하게 copy에 nums를 [깊은 복사](https://en.wikipedia.org/wiki/Object_copying#:~:text=Deep%20copy%20is%20a%20process,objects%20found%20in%20the%20original.&text=It%20means%20that%20any%20changes,reflect%20in%20the%20original%20object.){:target="_blank"}하여 넣어준다.
- nums로 복사된 copy를 반환한다.

5. 메서드인 int[] suffle()을 완성한다 
- copy 객체를 반복하여 내부 값들을 섞어준다.
  - num에 0에서 $idx + 1$번째 값 사이의 임의 값을 넣어준다.
  - num번째 값과 idx번째 값을 바꿔준다.
- 반복이 완료되면 값을 섞은 copy를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ShuffleAnArray.java){:target="_blank"}에서 확인 가능합니다.