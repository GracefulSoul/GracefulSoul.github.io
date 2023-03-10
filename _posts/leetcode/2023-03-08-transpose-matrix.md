---
title: "Leetcode Java Transpose Matrix"
excerpt: "Leetcode Transpose Matrix Java"
last_modified_at: 2023-03-08T20:00:00
header:
  image: /assets/images/leetcode/transpose-matrix.png
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
[Link](https://leetcode.com/problems/transpose-matrix){:target="_blank"}

# 코드
```java
class Solution {

	public int[][] transpose(int[][] matrix) {
		int row = matrix.length;
		int col = matrix[0].length;
		int[][] result = new int[col][row];
		for (int j = 0; j < col; j++) {
			for (int i = 0; i < row; i++) {
				result[j][i] = matrix[i][j];
			}
		}
		return result;
	}

}
```

# 결과
[Link](https://leetcode.com/problems/transpose-matrix/submissions/911411264/){:target="_blank"}

# 설명
1. matrix의 행과 열의 인덱스를 전환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- row는 matrix의 행의 개수를 저장한 변수이다.
- col은 matrix의 열의 개수를 저장한 변수이다.
- result는 matrix의 행과 열의 인덱스를 전환하여 저장할 배열로, $col \times row$ 크기의 2차원 정수 배열로 초기화한다.

3. 0부터 col미만까지 j를 증가시키고, 0부터 row미만까지 i를 증가시키며, result[j][i]의 위치에 matrix[i][j]의 값을 넣어준다.

4. 반복이 완료되면 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/TransposeMatrix.java){:target="_blank"}에서 확인 가능합니다.