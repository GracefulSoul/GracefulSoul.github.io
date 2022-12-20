---
title: "Leetcode Java Jewels and Stones"
excerpt: "Leetcode Jewels and Stones Java"
last_modified_at: 2022-12-20T02:30:00
header:
  image: /assets/images/leetcode/jewels-and-stones.png
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
[Link](https://leetcode.com/problems/jewels-and-stones){:target="_blank"}

# 코드
```java
class Solution {

  public int numJewelsInStones(String jewels, String stones) {
    int count = 0;
    for (char c : stones.toCharArray()) {
      if (jewels.indexOf(c) != -1) {
        count++;
      }
    }
    return count;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/jewels-and-stones/submissions/862491355/){:target="_blank"}

# 설명
1. 보석의 종류인 jewels를 이용하여 stones 내 몇 개의 보석이 포함되었는지 찾는 문제이다.

2. count는 stones 내 보석의 갯수를 저장할 변수이다.

3. stones의 모든 문자들을 이용하여 jewels에 포함된 단어가 있으면 count를 증가시킨다.

4. 반복이 완료되면 stones 내 보석의 갯수인 count를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/JewelsAndStones.java){:target="_blank"}에서 확인 가능합니다.