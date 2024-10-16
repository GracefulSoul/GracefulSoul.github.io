---
title: "Leetcode Java Find the Student that Will Replace the Chalk"
excerpt: "Leetcode Find the Student that Will Replace the Chalk Java"
last_modified_at: 2024-09-02T18:00:00
header:
  image: /assets/images/leetcode/find-the-student-that-will-replace-the-chalk.png
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
[Link](https://leetcode.com/problems/find-the-student-that-will-replace-the-chalk/){:target="_blank"}

# 코드
```java
class Solution {

  public int chalkReplacer(int[] chalk, int k) {
    long sum = 0;
    for (int c : chalk) {
      sum += c;
    }
    k %= sum;
    for (int i = 0; i < chalk.length; i++) {
      if ((k -= chalk[i]) < 0) {
        return i;
      }
    }
    return -1;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/convert-1d-array-into-2d-array/submissions/1374736202/){:target="_blank"}

# 설명
1. 각 학생 별 문제 풀이에 필요한 분필의 갯수가 저장된 chalk를 이용하여 k개의 분필을 모두 사용할 때, 마지막으로 사용할 학생 위치를 반환하는 문제이다.

2. sum은 학생들이 한 번씩 문제를 풀 때 필요한 분필의 갯수를 저장할 변수로, chalk의 분필 갯수를 모두 더해서 넣어준다.

3. k에 k를 sum을 나눈 나머지인 반복으로 소모되는 분필을 제거한 갯수를 넣어준다.

4. 0부터 chalk의 길이 미만까지 i를 증가시키면서 k에 chalk[i]의 값을 빼줄 때 0보다 작아지는 위치를 찾아 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindTheStudentThatWillReplaceTheChalk.java){:target="_blank"}에서 확인 가능합니다.