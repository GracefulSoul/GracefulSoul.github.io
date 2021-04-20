---
title: "Leetcode Java Container With Most Water"
excerpt: "Leetcode Container With Most Water Java 풀이"
last_modified_at: 2021-04-19T20:20:00
header:
  image: /assets/images/leetcode/container-with-most-water.png
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
[Link](https://leetcode.com/problems/container-with-most-water/)

# 코드
```java
class Solution {

	public int maxArea(int[] height) {
		int start = 0;
		int end = height.length - 1;
		int max = 0;
		while (start < end) {
			max = Math.max(max, Math.min(height[start], height[end]) * (end - start));
			if (height[start] < height[end]) {
				start++;
			} else {
				end--;
			}
		}
		return max;
	}

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/482578956/)

# 설명
1. 주어진 배열 height의 양 끝단부터 탐색하기 위해 초기 index인 start는 0, end는 height.length - 1로 초기화 한다.

2. 두 index인 start와 end 사이에 최대로 담을 수 있는 물의 양을 저장하기 위해 max 변수를 선언한다.

3. start 변수의 값이 end 변수의 값보다 같아지기 전까지 반복을 통해 최대로 담을 수 있는 물의 양을 탐색한다.
	- 두 index 사이에서 최대로 담을 수 있는 물의 양은 height[start]와 height[end]의 값 중 작은 값에서 end와 start의 길이만큼을 곱해주면된다.
	- 위의 물의 양과 최대로 담을 수 있는 물의 양을 저장한 변수 max와 비교하여 최대 값만 저장한다.

4. 만일 height[start]의 값이 height[end]을 분석하여 한칸씩 가운데로 이동한다.
	- 두 index 중 한 height[index] 값이 작으면 해당 값 위주로 배수를 곱하므로, 작은 값의 index를 이동하여 최대로 담을 수 있는 물의 양을 다시 탐색하기 위함이다.

5. 반복이 끝나면 최대로 담을 수 있는 물의 양을 저장한 max 변수를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ContainerWithMostWater.java)에서 확인 가능합니다.