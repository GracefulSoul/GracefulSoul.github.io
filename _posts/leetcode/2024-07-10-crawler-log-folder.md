---
title: "Leetcode Java Crawler Log Folder"
excerpt: "Leetcode Easy - 'Crawler Log Folder' 문제 Java 풀이"
last_modified_at: 2024-07-10T17:50:00
header:
  image: /assets/images/leetcode/crawler-log-folder.png
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
[Link](https://leetcode.com/problems/crawler-log-folder/){:target="_blank"}

# 코드
```java
class Solution {

  public int minOperations(String[] logs) {
    int result = 0;
    for (String log : logs) {
      switch (log) {
        case "../": result = Math.max(0, --result); break;
        case "./": break;
        default: result++; break;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/crawler-log-folder/submissions/1316181068/){:target="_blank"}

# 설명
1. 최상위 디렉토리에서 logs의 커맨드를 순차적으로 모두 입력했을 때, 위치한 폴더의 깊이를 반환하는 문제이다.

2. result는 위치한 폴더의 깊이를 저장할 변수로, 초기 위치인 0으로 초기화한다.

3. logs의 각 값을 log에 넣어 순차적으로 아래를 수행한다.
- log가 "../"인 경우, 최상위 디렉토리의 위치인 0과 result에서 1 감소한 값 중 큰 값을 넣어준다.
- log가 "./"인 경우, 무시하고 다음 반복을 수행한다.
- 그 외의 모든 경우에는 하위 폴더로 이동하므로, result를 증가시켜준다.

4. 반복이 완료되면 깊이가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CrawlerLogFolder.java){:target="_blank"}에서 확인 가능합니다.