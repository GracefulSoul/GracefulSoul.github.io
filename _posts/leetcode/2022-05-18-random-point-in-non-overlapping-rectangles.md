---
title: "Leetcode Java Random Point in Non-overlapping Rectangles"
excerpt: "Leetcode Random Point in Non-overlapping Rectangles"
last_modified_at: 2022-05-18T12:00:00
header:
  image: /assets/images/leetcode/random-point-in-non-overlapping-rectangles.png
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
[Link](https://leetcode.com/problems/random-point-in-non-overlapping-rectangles/){:target="_blank"}

# 코드
```java
class Solution {

	private TreeMap<Integer, Integer> map;
	private int sum;
	private int[][] rectangles;
	private Random random;

	public Solution(int[][] rects) {
		this.sum = 0;
		this.map = new TreeMap<>();
		this.rectangles = rects;
		this.random = new Random();
		for (int idx = 0; idx < rects.length; idx++) {
			this.sum += (rects[idx][2] - rects[idx][0] + 1) * (rects[idx][3] - rects[idx][1] + 1);
			this.map.put(this.sum, idx);
		}
	}

	public int[] pick() {
		int index = this.map.ceilingEntry(1 + this.random.nextInt(this.sum)).getValue();
		int x = this.random.nextInt(this.rectangles[index][2] - this.rectangles[index][0] + 1);
		int y = this.random.nextInt(this.rectangles[index][3] - this.rectangles[index][1] + 1);
		return new int[] { this.rectangles[index][0] + x, this.rectangles[index][1] + y };
	}

}

/**
 * Your Solution object will be instantiated and called as such:
 * Solution obj = new Solution(rects);
 * int[] param_1 = obj.pick();
 */
```

# 결과
[Link](https://leetcode.com/submissions/detail/701812745/){:target="_blank"}

# 설명
1. 겹치지 않은 사각형의 위치인 rects 내 임의의 점의 위치를 반환하는 문제이다.
- 생성자인 Solution(int[][] rects)은 사각형의 좌표인 rects를 이용하여 객체를 초기화하는 역할을 수행한다.
- 메서드인 pick()은 생성자를 통해 주입된 rects 내 임의 점을 생성하여 해당 좌표를 [x, y] 배열로 반환하는 역할을 수행한다.

2. 문제 풀이에 필요한 전역 변수를 정의한다.
- map은 사각형의 면적 별 rects 내 사각형의 위치 값을 저장하여 보관할 변수로, 키에 대한 메서드 활용을 위해서 TreeMap으로 정의한다.
- sum은 사각형의 면적의 합을 저장할 변수이다.
- rectangles는 생성자를 통해 주입된 rects를 보관할 변수이다.
- random은 임의 좌표를 생성하기 위해 활용될 변수이다.

3. 생성자인 Solution(int[][] rects)을 정의한다.
- sum을 0으로, map을 새 TreeMap 객체를 생성하여 초기화한다.
- rectangles에 주어진 rects 배열을 넣어준다.
- random 객체를 임의 숫자 생성을 위한 Random 객체를 생성하여 초기화한다.
- 0부터 rects 배열의 길이 미만까지 idx를 증가시키며 아래를 수행한다.
  - sum에 rects의 idx번째 사각형의 면적을 계산하여 넣어주고, map에 key가 sum이고 value는 idx로 넣어준다.

4. 메서드인 메서드인 pick()을 정의한다.
- map에서 1부터 sum 이하의 숫자를 생성하여 해당 값보다 작은 key 중 가장 인접한 key의 value를 꺼내 index에 넣어준다.
- rectangles 내 index번째 값을 가져와 rectangle로 정의한다.
- x에 rectangle의 0에서 x축 길이 내 임의의 값을 넣어준다.
- y에 rectangle의 0에서 y축 길이 내 임의의 값을 넣어준다.
- rectangle의 x축 위치에 x를 더하고, y축 위치에 y를 더한 값들을 정수 배열로 만들어 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/object/solution/random/point/rectangle/Solution.java){:target="_blank"}에서 확인 가능합니다.