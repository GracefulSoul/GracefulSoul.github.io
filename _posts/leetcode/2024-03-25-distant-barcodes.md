---
title: "Leetcode Java Distant Barcodes"
excerpt: "Leetcode Medium - 'Distant Barcodes' 문제 Java 풀이"
last_modified_at: 2024-03-25T19:00:00
header:
  image: /assets/images/leetcode/distant-barcodes.png
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
[Link](https://leetcode.com/problems/distant-barcodes/){:target="_blank"}

# 코드
```java
class Solution {

  public int[] rearrangeBarcodes(int[] barcodes) {
    int length = barcodes.length;
    for (int i = 1; i < length; i++) {
      if (barcodes[i] == barcodes[i - 1]) {
        int j = i + 1;
        while (j < length && barcodes[i] == barcodes[j]) {
          j++;
        }
        if (j < length) {
          barcodes[i] = barcodes[j];
          barcodes[j] = barcodes[i - 1];
        }
      }
    }
    for (int i = length - 2; i >= 0; i--) {
      if (barcodes[i] == barcodes[i + 1]) {
        int j = i - 1;
        while (j >= 0 && barcodes[j] == barcodes[i]) {
          j--;
        }
        if (j >= 0) {
          barcodes[i] = barcodes[j];
          barcodes[j] = barcodes[i + 1];
        }
      }
    }
    return barcodes;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/distant-barcodes/submissions/1213348032/){:target="_blank"}

# 설명
1. barcodes의 각 숫자들의 인접한 숫자들끼리 동일하지 않은 값으로 재배치하는 문제이다.

2. length는 barcodes의 길이를 저장한 변수이다.

3. 1부터 length까지 i를 증가시키며 barcodes의 앞에서 뒤 순서로 아래를 반복하여 순서를 다시 섞어준다.
- barcodes의 i번째 값과 $i - 1$번째 값이 동일한 경우, 아래를 수행한다.
  - j는 바꿀 값의 위치를 저장할 변수로, $i + 1$로 초기화하여 j가 length 미만이면서 barcodes의 i번째 자리의 값과 j번째 자리의 값이 동일할 때 까지 j를 증가시켜준다.
  - j가 length 미만인 값을 찾은 경우, barcodes의 i번째 위치에 j번째 값을 j번째 위치에 $i + 1$번째 값을 넣어 값을 섞어준다.

4. $length - 2$부터 0 이상일 때 까지 i를 감소시키며 barcodes의 뒤에서 앞 순서를 아래를 반복하여 순서를 다시 섞어준다.
- barcodes의 i번째 값과 $i + 1$번째 값이 동일한 경우, 아래를 수행한다.
  - j는 바꿀 값의 위치를 저장할 변수로, $i - 1$로 초기화하여 j가 0 이상이면서 barcodes의 j번째 자리의 값과 i번째 자리의 값이 동일할 때 까지 j를 감소시켜준다.
  - j가 0 이상인 경우 값을 찾은 경우, barcodes의 i번째 위치에 j번째 값을 j번째 위치에 $i + 1$번째 값을 넣어 값을 섞어준다.

5. 위의 두 반복이 완료되어 동일한 값이 인접하지 않도록 섞은 barcodes를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DistantBarcodes.java){:target="_blank"}에서 확인 가능합니다.