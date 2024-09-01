---
title: "Leetcode Java Convert 1D Array Into 2D Array"
excerpt: "Leetcode Convert 1D Array Into 2D Array Java"
last_modified_at: 2024-09-01T09:50:00
header:
  image: /assets/images/leetcode/convert-1d-array-into-2d-array.png
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
[Link](https://leetcode.com/problems/convert-1d-array-into-2d-array/){:target="_blank"}

# 코드
```java
class Solution {

	public int[][] construct2DArray(int[] original, int m, int n) {
		if (original.length == m * n) {
			int[][] result = new int[m][n];
			for (int i = 0; i < original.length; i++) {
				result[i / n][i % n] = original[i];
			}
			return result;
		} else {
			return new int[0][0];
		}
	}

}
```

# 결과
[Link](https://leetcode.com/problems/convert-1d-array-into-2d-array/submissions/1374736202/){:target="_blank"}

# 설명
1. original 배열을 $m \times n$ 크기의 배열로 변환하는 문제이다.
- 단, 변환이 불가능한 경우 빈 배열을 반환한다.

2. original의 길이와 $m \times n $이 동일한 경우, 아래를 수행하여 $m \times n$ 크기의 배열로 변환하여 주어진 문제의 결과로 반환한다.
- result를 $m \times n$ 크기의 배열로 정의한다.
- 0부터 original의 길이 미만까지 i를 증가시키며 n개씩 넣어야 하므로, result의 $\frac{i}{n}$의 몫에 해당하는 행의 나머지에 해당하는 열에 original[i]를 넣어준다.
- 변환된 result를 주어진 문제의 결과로 반환한다.

3. original의 길이와 $m \times n $이 동일하지 않은 경우, 빈 2차원 배열을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/Convert1DArrayInto2DArray.java){:target="_blank"}에서 확인 가능합니다.