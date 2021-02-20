---
title: "Codility Binary Gap"
excerpt: "Lesson1. Binary Gap"
last_modified_at: 2021-02-20T13:49:00
header:
  image: /assets/images/codility/BinaryGap.jpg
categories:
  - Programming
tags:
  - Programming
  - Coding Test
  - Binary

toc: true
toc_ads: true
toc_sticky: true
---
# 문제
A binary gap within a positive integer N is any maximal sequence of consecutive zeros that is surrounded by ones at both ends in the binary representation of N.

For example, number 9 has binary representation 1001 and contains a binary gap of length 2. The number 529 has binary representation 1000010001 and contains two binary gaps: one of length 4 and one of length 3. The number 20 has binary representation 10100 and contains one binary gap of length 1. The number 15 has binary representation 1111 and has no binary gaps. The number 32 has binary representation 100000 and has no binary gaps.

Write a function:
```java
class Solution { public int solution(int N); }
```
that, given a positive integer N, returns the length of its longest binary gap. The function should return 0 if N doesn't contain a binary gap.

For example, given N = 1041 the function should return 5, because N has binary representation 10000010001 and so its longest binary gap is of length 5. Given N = 32 the function should return 0, because N has binary representation '100000' and thus no binary gaps.

Write an efficient algorithm for the following assumptions:

- N is an integer within the range [1..2,147,483,647].
Copyright 2009–2021 by Codility Limited. All Rights Reserved. Unauthorized copying, publication or disclosure prohibited.

# 코드
```java
// you can also use imports, for example:
// import java.util.*;

// you can write to stdout for debugging purposes, e.g.
// System.out.println("this is a debug message");

class Solution {
    public int solution(int N) {
        char[] binary = Integer.toBinaryString(N).toCharArray();
        int max = 0;
        int counter = 0;
        // Loop and check max length.
        for (int idx = 1; idx < binary.length; idx++) {
            if(binary[idx] == '0') {
                counter++;
            } else {
                if (counter > max) {
                    max = counter;
                }
                // Initializing counter.
                counter = 0;
            }
        }
        return max;
    }
}
```

# 설명
1. 주어진 숫자를 Binary로 변환한다.
2. Binary를 순차 확인하며, 1사이의 0의 갯수를 센다.
- Binary의 시작은 항상 1부터로, Index 1부터 탐색한다.
- 1이 나타날 경우 max에 임시 저장하고, counter를 초기화하여 다시 갯수를 센다.
3. max값을 return하여 주어진 문제의 결과를 반환한다.

# 소스
[GitHub-BinaryGap](https://github.com/GracefulSoul/Sample/blob/master/src/main/java/gracefulsoul/codility/lesson01/BinaryGap.java)