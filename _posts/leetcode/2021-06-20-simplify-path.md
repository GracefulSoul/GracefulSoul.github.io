---
title: "Leetcode Java Simplify Path"
excerpt: "Leetcode - 'Simplify Path' 문제 Java 풀이"
last_modified_at: 2021-06-20T14:40:00
header:
  image: /assets/images/leetcode/simplify-path.png
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
[Link](https://leetcode.com/problems/simplify-path/){:target="_blank"}

# 코드
```java
class Solution {

  public String simplifyPath(String path) {
    Stack<String> stack = new Stack<>();
    for (String directory : path.split("/")) {
      switch (directory) {
        case "":case ".": continue;
        case "..": this.popStackIsNotEmpty(stack); break;
        default: stack.push(directory);
      }
    }
    return this.getPath(stack);
  }

  private void popStackIsNotEmpty(Stack<String> stack) {
    if (!stack.isEmpty()) {
      stack.pop();
    }
  }

  private String getPath(Stack<String> stack) {
    StringBuilder sb = new StringBuilder();
    for (String directory : stack) {
      sb.append("/").append(directory);
    }
    return sb.length() == 0 ? "/" : sb.toString();
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/510478995/){:target="_blank"}

# 설명
1. 주어진 문자열 File path에 대한 절대 경로를 단순화된 표준 경로를 구하는 문제이다.

2. 단순화된 표준 경로를 구하기 위해 변수 stack을 정의한다.

3. 주어진 변수 path를 "/"를 구분자로 디렉토리 이름인 문자열을 분리하여 반복하여 단순화된 표준 경로를 구한다.
- 디렉토리 명이 ""이거나 "."일 경우, 무시하고 계속 반복한다.
- 디렉토리 명이 ".."일 경우, 상위 경로를 의미하므로 stack이 비어있지 않은 경우에만 최근 값을 꺼낸다.
- 그 외의 경우, 디렉토리 이름을 stack에 저장한다.

4. 3번을 통해 표준 경로를 만들기 위한 디렉토리 이름이 저장된 stack을 이용하여 아래 규칙을 만족하는 단순화된 표준 경로를 만든다.
- Path의 첫 시작은 "/"으로 시작해야 한다.
- 각 디렉토리는 "/"로 구분된다.
- 경로의 마지막은 "/"로 끝나지 않는다.
- 경로는 루트 디렉터리에서 대상이 되는 파일 혹은 디렉터리로의 경로만 포함된다.

5. 4번을 통해 조합된 단순화된 표준 경로를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SimplifyPath.java){:target="_blank"}에서 확인 가능합니다.