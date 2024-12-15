---
title: "Leetcode Java Maximum Average Pass Ratio"
excerpt: "Leetcode - 'Maximum Average Pass Ratio' 문제 Java 풀이"
last_modified_at: 2024-12-15T12:00:00
header:
  image: /assets/images/leetcode/maximum-average-pass-ratio.png
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
[Link](https://leetcode.com/problems/maximum-average-pass-ratio/){:target="_blank"}

# 코드
```java
class Solution {

  public double maxAverageRatio(int[][] classes, int extraStudents) {
    Queue<double[]> queue = new PriorityQueue<>(Comparator.comparingDouble(c -> -c[2]));
    for (int[] c : classes) {
      double a = c[0];
      double b = c[1];
      queue.offer(new double[] { a, b, this.getRatio(a, b) });
    }
    while (extraStudents-- > 0) {
      double[] curr = queue.poll();
      double a = curr[0];
      double b = curr[1];
      queue.offer(new double[] { a + 1, b + 1, this.getRatio(a + 1, b + 1) });
    }
    double result = 0.0d;
    while (!queue.isEmpty()) {
      double[] curr = queue.poll();
      result += curr[0] / curr[1];
    }
    return result / classes.length;
  }

  private double getRatio(double a, double b) {
    return ((a + 1) / (b + 1)) - (a / b);
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximum-average-pass-ratio/submissions/1479096096/){:target="_blank"}

# 설명
1. 아래의 규칙으로 구성된 classes로 extraStudents를 추가 배정하여 가능한 최대 평균 합격률을 구하는 문제이다.
- classes[i] = [pass<sub>i</sub>, total<sub>i</sub>]로, total인원 중 pass만큼의 인원만 합격 가능하다.
- 학급의 합격률은 시험에 합격할 학생 수를 총 학생 수로 나눈 값이다.
- 평균 합격률은 모든 학급의 합격률을 학급의 수로 나눈 값이다.

2. 합격할 학생의 수인 a와 총 학생의 수인 b를 이용하여 한 학생이 추가되는 경우, 추가될 합격률을 구하기 위한 getRatio(double a, double b)를 정의한다.
- $\frac{a + 1}{b + 1}$에 $\frac{a}{b}$를 뺀 값을 반환한다.

3. queue는 합격률을 기준으로 정렬하여 저장할 변수로, PriorityQueue로 초기화 후 classes[i][0], classes[i][1], 2번에서 정의한 getRatio(double a, double b)메서드에 앞의 두 값을 수행한 결과 세 값을 배열로 넣어준다.

4. extraStudents가 0 초과일 때 까지 아래를 수행 후 extraStudents를 감소시켜준다.
- curr에 queue의 맨 앞값을 꺼내준다.
- queue에 $a + 1$, $b + 1$, 2번에서 정의한 getRatio(double a, double b)메서드에 앞의 두 값을 수행한 결과 세 값을 배열로 넣어준다.

5. 결과를 넣을 result를 정의하고, queue를 반복하여 합격할 학생의 수인 첫 번째 값에 총 학생의 수인 두 번째 값을 나눈 결과를 더해준다.

6. 앞에서 더한 결과를 classes의 길이인 학급의 수로 나눈 평균 합격률을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumAveragePassRatio.java){:target="_blank"}에서 확인 가능합니다.