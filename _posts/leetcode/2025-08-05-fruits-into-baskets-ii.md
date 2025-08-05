---
title: "Leetcode Java Fruits Into Baskets II"
excerpt: "Leetcode - 'Fruits Into Baskets II' 문제 Java 풀이"
last_modified_at: 2025-08-05T19:30:00
header:
  image: /assets/images/leetcode/fruits-into-baskets-ii.png
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
[Link](https://leetcode.com/problems/fruits-into-baskets-ii/){:target="_blank"}

# 코드
```java
class Solution {

  public int numOfUnplacedFruits(int[] fruits, int[] baskets) {
    int length = fruits.length;
    int result = length;
    for (int i = 0; i < length; i++) {
      for (int j = 0; j < length; j++) {
        if (fruits[i] <= baskets[j]) {
          baskets[j] = 0;
          result--;
          break;
        }
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/fruits-into-baskets-ii/submissions/1724223950/){:target="_blank"}

# 설명
1. 각 자릿수에 해당하는 유형의 과일들의 갯수가 저장된 fruits와 과일을 담을 수 있는 갯수 별 바구니들인 baskets를 이용하여 아래를 수행한 후 담지 못한 과일의 갯수를 계산하는 문제이다.
- fruits[i]는 baskets에서 해당 과일을 담을 수 있는 동일한 크기 혹은 더 큰 크기의 바구니를 좌측부터 찾아 조건을 만족하는 빈 바구니가 존재하면 해당 바구니에 해당 과일을 담는다.
- 한 유형의 과일을 담은 바구니에 다른 유형의 과일을 추가로 담을 수 없다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 fruits의 길이을 저장한 변수이다.
- result는 담을 수 없는 과일의 갯수를 저장한 변수로, 가능한 최대 갯수인 length로 초기화한다.

3. 0부터 length 미만까지 i를 증가시키며 아래를 반복한다.
- 다시 0부터 length 미만까지 j를 증가시키며 아래를 반복한다.
  - fruits[i]의 값이 baskets[j] 이하인 조건에 만족하는 바구니인 경우, baskets[j]의 값을 0으로 바꿔 사용한 바구니임을 체크하고 result를 감소신 후 다음 반복을 수행한다.

4. 반복이 완료되면 담을 수 없는 과일의 갯수가 남은 result를 주어진 무제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FruitsIntoBasketsII.java){:target="_blank"}에서 확인 가능합니다.