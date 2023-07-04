---
title: "Leetcode Java Valid Mountain Array"
excerpt: "Leetcode Valid Mountain Array Java"
last_modified_at: 2023-07-04T19:20:00
header:
  image: /assets/images/leetcode/valid-mountain-array.png
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
[Link](https://leetcode.com/problems/valid-mountain-array){:target="_blank"}

# 코드
```java
class Solution {

  public boolean validMountainArray(int[] arr) {
    if (arr.length < 3 || arr[0] >= arr[1]) {
      return false;
    }
    boolean decrease = false;
    for (int i = 2; i < arr.length; i++) {
      if (arr[i - 1] > arr[i]) {
        decrease = true;
      } else if (arr[i - 1] == arr[i] || decrease) {
        return false;
      }
    }
    return decrease;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/valid-mountain-array/submissions/986026006/){:target="_blank"}

# 설명
1. 산의 높이로 이루어진 arr의 값들이 아래의 조건을 만족하는 산 모양으로 이루어져 있는지 검증하는 문제이다.
- arr의 길이가 3 이상이어야 산 모양을 유지할 수 있다.
- 산 정상인 i번째 위치 이전과 이후는 점층적인 값의 증가와 감소로만 이루어져야 한다.

2. arr의 길이가 3 미만이거나 arr의 첫 값이 다음 값보다 크거나 같으면, 산 모양을 이룰 수 없으므로 false를 주어진 문제의 결과로 반환한다.

3. decrease는 점층적으로 감소하는 추세로 변환되었는지 저장하기 위한 변수로, 처음은 점층적으로 증가해야 하므로 false를 넣어준다.

4. 2부터 arr의 길이 미만까지 i를 증가시키며 아래를 검증한다.
- arr의 $i - 1$번째 값이 i번째 값보다 크면, 감소하는 추세로 변화하였으므로 decrease에 true를 넣어준다.
- arr의 $i - 1$번째 값과 i번째 값이 동일하거나 decrease가 true이면, 조건을 만족하는 산의 모양을 유지하지 않으므로 false를 주어진 문제의 결과로 반환한다.

5. 반복이 완료되면 감소하는 추세가 계속 유지했는지 여부인 decrease의 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ValidMountainArray.java){:target="_blank"}에서 확인 가능합니다.