---
title: "Leetcode Java Statistics from a Large Sample"
excerpt: "Leetcode Medium - 'Statistics from a Large Sample' 문제 Java 풀이"
last_modified_at: 2024-04-27T18:40:00
header:
  image: /assets/images/leetcode/statistics-from-a-large-sample.png
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
[Link](https://leetcode.com/problems/statistics-from-a-large-sample/){:target="_blank"}

# 코드
```java
class Solution {

  public double[] sampleStats(int[] count) {
    double[] result = new double[] { 256, -1, 0, 0, 0 };
    int left = 0;
    int right = 255;
    int count1 = 0;
    int count2 = 0;
    int mid1 = 0;
    int mid2 = 0;
    for (int i = 0; i < count.length; i++) {
      if (count[i] > 0) {
        if (result[0] == 256) {
          result[0] = i;
        }
        result[1] = i;
        result[2] += (double) i * count[i];
        if (count[i] > count[(int) result[4]]) {
          result[4] = i;
        }
      }
    }
    while (left <= right) {
      while (count[left] == 0) {
        left++;
      }
      while (count[right] == 0) {
        right--;
      }
      if (count1 < count2) {
        count1 += count[left];
        mid1 = left++;
      } else {
        count2 += count[right];
        mid2 = right--;
      }
    }
    result[2] /= (count1 + count2);
    if (count1 < count2) {
      result[3] = mid2;
    } else if (count1 > count2) {
      result[3] = mid1;
    } else {
      result[3] = (mid1 + mid2) / 2.0;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/statistics-from-a-large-sample/submissions/1243187317/){:target="_blank"}

# 설명
1. [0, 255] 범위 내 숫자들의 갯수를 저장한 count를 이용하여 순차적으로 [최솟값, 최댓값, 평균값, 중앙값, 최빈값]을 구하여 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 결과를 저장할 변수로, 순차적으로 아래의 의미를 가진 값을 넣어준다.
  - 첫 번째 값은 최솟값으로, 최대 위치 값보다 1 큰 256을 넣어준다.
  - 두 번째 값은 최댓값으로, 최소 위치 값보다 1 작은 -1을 넣어준다.
  - 나머지는 순서대로 평균값, 중앙값, 최빈값으로 모두 0을 넣어준다.
- left와 right는 숫자 위치를 저장할 변수로, 값에 대한 인덱스의 최솟값과 최댓값의 0과 255로 초기화한다.
- count1과 count2는 count의 좌측과 우측의 갯수를 계산할 변수로, 둘 다 0으로 초기화한다.
- mid1과 mid2는 중앙값 계산을 count1과 count2에 따라 계산할 변수로, 둘 다 0으로 초기화한다.

3. 0부터 count의 길이 미만까지 i를 증가시키며 아래를 반복한다.
- count[i]의 값이 0보다 큰 갯수가 존재하는 경우만 수행을 진행한다.
- result[0]의 값인 최솟값이 256인 초기값인 경우, 해당 위치에 i를 넣어준다.
- result[1]의 값인 최댓값을 i로 갱신해준다.
- result[2]의 값인 평균값을 구하기 위한 값에 i를 실수로 변환하여 count[i]와 곱한 결과를 넣어준다.
- count[i]의 값인 최빈값보다 count[result[4]]의 값보다 크다면, 해당 값으로 최빈값을 수정해준다.

4. left가 right보다 작거나 같을 때 까지 아래를 반복한다.
- count[left]가 0이 아닐 때 까지 left를 증가시키고, count[right]가 0이 아닐 때 까지 right를 감소시킨다.
- count1이 count2보다 작은 경우, 아래를 수행한다.
  - count1에 count[left]의 값을 더해준다.
  - mid1에 left를 넣고 left를 증가시켜준다.
- count1이 count2보다 작지 않은 경우, 아래를 수행한다.
  - count2에 count[right]의 값을 더해준다.
  - mid2에 right를 넣고 right를 감소시켜준다.

5. 위의 반복이 완료되면 result[2]인 평균값에 $count1 + count2$ 값을 더해서 해당 값에 나눠주어 평균값을 계산해준다.

6. count1과 count2의 크기에 따라 중앙값을 넣어준다.
- count1이 count2보다 작은 경우 mid2의 값이 중앙값이므로, result[3]에 mid2를 넣어준다.
- count1이 count2보다 큰 경우 mid1의 값이 중앙값이므로, result[3]에 mid1을 넣어준다.
- 두 경우가 아니라면, result[3]에 $frac{mid1 + mid2}{2}$의 값을 실수형태로 계산하여 넣어준다.

7. 반복이 완료되면 모든 결과가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/StatisticsFromALargeSample.java){:target="_blank"}에서 확인 가능합니다.