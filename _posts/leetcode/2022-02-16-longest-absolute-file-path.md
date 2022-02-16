---
title: "Leetcode Java Longest Absolute File Path"
excerpt: "Leetcode Longest Absolute File Path Java 풀이"
last_modified_at: 2022-02-16T12:00:00
header:
  image: /assets/images/leetcode/longest-absolute-file-path.png
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
[Link](https://leetcode.com/problems/longest-absolute-file-path/){:target="_blank"}

# 코드
```java
class Solution {

  public int lengthLongestPath(String input) {
    String[] paths = input.split("\n");
    int[] stack = new int[paths.length + 1];
    int result = 0;
    for (String path : paths) {
      int level = path.lastIndexOf("\t") + 1;
      int curr = stack[level + 1] = stack[level] + path.length() - level + 1;
      if (path.contains(".")) {
        result = Math.max(result, curr - 1);
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/642270544/){:target="_blank"}

# 설명
1. Directory Path인 input을 이용하여 dir부터 가장 긴 디렉토리 구조의 길이를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- paths에 input의 폴더 구분인 "\n"로 분리하여 문자열의 배열로 넣어준다.
- stack에는 이전까지 디렉토리 구조의 길이를 넣어줄 정수 배열로, $paths.legnth + 1$ 크기로 정의한다.
- result는 가장 긴 디렉토리 구조의 길이를 넣을 변수로, 0으로 초기화한다.

3. paths를 반복하여 result에 결과를 넣어준다.
- level에 폴더 혹은 파일 이름의 시작이되는 path의 마지막 "\t"의 위치 값을 넣어준다.
- curr과 stack[$level + 1$]에 path에 해당하는 디렉토리 구조의 길이인 $stack[level] + path.length - level + 1$를 넣어준다.
- path에 파일 확장자의 구분이 되는 콤마(".")가 존재한다면, result에 result와 $curr - 1$ 중 큰 값을 넣어준다.

4. 반복이 완료되면 가장 긴 디렉토리 구조의 길이를 저장한 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LongestAbsoluteFilePath.java){:target="_blank"}에서 확인 가능합니다.