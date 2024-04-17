---
title: "Leetcode Java Smallest Duplicate Zeros"
excerpt: "Leetcode Smallest Duplicate Zeros Java"
last_modified_at: 2024-04-17T18:30:00
header:
  image: /assets/images/leetcode/duplicate-zeros.png
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
[Link](https://leetcode.com/problems/duplicate-zeros/){:target="_blank"}

# 코드
```java
class Solution {

  public void duplicateZeros(int[] arr) {
    int i = 0;
    int count = 0;
    int length = arr.length;
    while (i + count < length) {
      if (arr[i++] == 0) {
        count++;
      }
    }
    for (i = i - 1; count > 0; i--) {
      if (i + count < length) {
        arr[i + count] = arr[i];
      }
      if (arr[i] == 0) {
        arr[i + --count] = arr[i];
      }
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/duplicate-zeros/submissions/1234735196/){:target="_blank"}

# 설명
1. 정수 배열 arr 내 0이 존재하면 다음 자리부터의 모든 값들을 한 칸 우측으로 밀고 해당 자리에 0을 넣어주는 문제이다.
- arr 크기를 벗어난 값은 그대로 제거된다.

2. 문제 풀이에 필요한 변수를 정의한다.
- i는 arr 내 탐색을 위한 위치 변수로 사용할 변수로, 0으로 초기화한다.
- count는 arr 내 0의 갯수를 계산하기 위한 변수로, arr의 값들을 처음부터 $i + count$인 arr에 포함될 값들의 위치까지 반복하여 0 갯수를 넣어준다.
- length는 arr의 길이를 저장한 변수이다.

3. $i - 1$부터 count가 0 초과일 때 까지 i를 감소시키며 아래를 반복한다.
- $i + count$가 length보다 작은 경우, arr[$i + count$] 위치에 arr[i]를 넣어 arr의 마지막부터 값을 옮겨준다.
- arr[i]의 값이 0인 경우, count를 감소시킨 후 arr[$i + count$] 위치에 arr[i]를 넣어 0을 이어준다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DuplicateZeros.java){:target="_blank"}에서 확인 가능합니다.