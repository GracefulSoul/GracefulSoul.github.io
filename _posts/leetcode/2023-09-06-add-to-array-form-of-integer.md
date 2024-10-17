---
title: "Leetcode Java Add to Array-Form of Integer"
excerpt: "Leetcode Easy - 'Add to Array-Form of Integer' 문제 Java 풀이"
last_modified_at: 2023-09-06T19:00:00
header:
  image: /assets/images/leetcode/add-to-array-form-of-integer.png
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
[Link](https://leetcode.com/problems/add-to-array-form-of-integer){:target="_blank"}

# 코드
```java
class Solution {

  public List<Integer> addToArrayForm(int[] num, int k) {
    LinkedList<Integer> result = new LinkedList<>();
    int length = num.length - 1;
    while (length >= 0 || k != 0) {
      if (length >= 0) {
        k += num[length--];
      }
      result.addFirst(k % 10);
      k /= 10;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/add-to-array-form-of-integer/submissions/1042011101/){:target="_blank"}

# 설명
1. 숫자로 이루어진 배열인 num을 이은 숫자와 k의 합을 한 숫자씩 잘라 반환하는 문제이다.

2. 문제 풀이에 필요한 변수이다.
- result는 결과를 한 숫자씩 이어 저장할 변수로, 값을 앞으로 넣어주기 위해 LinkedList로 초기화한다.
- length는 num의 길이를 저장한 변수이다.

3. length가 0 이상이거나 k가 0이 아닐 때 까지 아래를 반복한다.
- length가 0 이상인 경우, k에 num[length] 값을 더해주고 length를 감소시킨다.
- result의 맨 앞에 k를 10으로 나누었을 때 나머지 값을, k에 몫 값을 넣어준다.

4. 반복이 완료되면 두 값을 더해서 숫자 하나씩 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/AddToArrayFormOfInteger.java){:target="_blank"}에서 확인 가능합니다.