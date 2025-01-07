---
title: "Leetcode Java Minimum Number of Operations to Move All Balls to Each Box"
excerpt: "Leetcode - 'Minimum Number of Operations to Move All Balls to Each Box' 문제 Java 풀이"
last_modified_at: 2025-01-06T19:30:00
header:
  image: /assets/images/leetcode/minimum-number-of-operations-to-move-all-balls-to-each-box.png
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
[Link](https://leetcode.com/problems/minimum-number-of-operations-to-move-all-balls-to-each-box/){:target="_blank"}

# 코드
```java
class Solution {

  public int[] minOperations(String boxes) {
    char[] charArray = boxes.toCharArray();
    int length = charArray.length;
    int[] result = new int[length];
    for (int i = 0, move = 0, count = 0; i < length; i++, move += count) {
      result[i] += move;
      if (charArray[i] == '1') {
        count++;
      }
    }
    for (int i = length - 1, move = 0, count = 0; i >= 0; i--, move += count) {
      result[i] += move;
      if (charArray[i] == '1') {
        count++;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-number-of-operations-to-move-all-balls-to-each-box/submissions/1499390094/){:target="_blank"}

# 설명
1. 각 위치에 존재하는 박스에 공이 존재하는지 여부가 담긴 boxes를 이용하여 해당 위치로 모든 공을 모으기위한 최소 이동 횟수를 구하는 문제이다.
- boxes[i]의 값 중 '1'은 공이 존재, '0'은 빈 박스를 의미한다.
- 공은 비어있는 박스로만 이동이 가능하다.

2. 문제 풀이에 필요한 변수를 정의한다.
- charArray는 boxes를 문자 배열로 변환한 변수이다.
- length는 charArray의 길이를 저장한 변수이다.
- result는 각 위치 별 최소 이동 횟수를 저장하기 위한 변수로, boxes와 동일한 length 길이로 초기화한다.

3. i는 0부터 length 미만까지, 이동 횟수인 move와 공의 갯수인 count는 0으로 초기화하여 각 수행 별 i를 증가시키고 move에 count를 더해가며 아래를 반복한다.
- result[i]에 이동 횟수인 move를 더해준 후, charArray[i]인 i번째 문자가 1인 공이 존재하면 count인 공의 갯수를 증가시켜준다.

4. i는 $length - 1$부터 0 이상까지, 이동 횟수인 move와 공의 갯수인 count는 0으로 초기화하여 각 수행 별 i를 감소시키고 move에 count를 더해가며 아래를 반복한다.
- result[i]에 이동 횟수인 move를 더해준 후, charArray[i]인 i번째 문자가 1인 공이 존재하면 count인 공의 갯수를 증가시켜준다.

5. 반복이 완료되면 좌측부터 우측으로, 우측부터 좌측으로 공의 이동 갯수를 계산한 결과가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumNumberOfOperationsToMoveAllBallsToEachBox.java){:target="_blank"}에서 확인 가능합니다.