---
title: "Leetcode Java Video Stitching"
excerpt: "Leetcode Video Stitching Java"
last_modified_at: 2024-01-19T19:20:00
header:
  image: /assets/images/leetcode/video-stitching.png
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
[Link](https://leetcode.com/problems/video-stitching){:target="_blank"}

# 코드
```java
class Solution {

  public int videoStitching(int[][] clips, int time) {
    int min = 0;
    int max = 0;
    int result = 0;
    while (max < time) {
      for (int i = 0; i < clips.length; i++) {
        int[] clip = clips[i];
        if (clip[0] <= min && clip[1] > max) {
          max = clip[1];
        }
      }
      if (min == max) {
        return -1;
      }
      min = max;
      result++;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/video-stitching/submissions/1150594976/){:target="_blank"}

# 설명
1. 비디오 클립이 담긴 clips를 이용하여 time까지 클립을 잇기 위한 최소 클립의 갯수를 구하는 문제이다.
- clips[i] = [start<sub>i</sub>, end<sub>i</sub>]를 만족한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- min과 max는 time까지 클립을 잇기 위한 클립을 구하기 위한 변수로, 둘 다 0으로 초기화한다.
- result는 최소 클립의 갯수를 저장할 변수로, 0으로 초기화한다.

3. max가 time 미만일 때 까지 아래를 반복한다.
- 0부터 clips의 길이 미만까지 i를 증가시키며 시작 값이 min 이하이거나 같고, 종료 값이 max 이상일 때, max에 종료 값을 넣어준다.
- min과 max가 동일하면 time까지 이어줄 수 없으므로 -1을 주어진 문제의 결과로 반환한다.
- 위의 경우가 아니라면 이어줄 클립이 존재하므로, min에 max를 넣어준 후 result를 증가시켜 클립의 수를 계산해준다.

4. 반복이 완료되면 최소 클립의 수가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/VideoStitching.java){:target="_blank"}에서 확인 가능합니다.