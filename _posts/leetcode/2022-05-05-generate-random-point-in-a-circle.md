---
title: "Leetcode Java Generate Random Point in a Circle"
excerpt: "Leetcode Generate Random Point in a Circle Java 풀이"
last_modified_at: 2022-05-05T17:00:00
header:
  image: /assets/images/leetcode/generate-random-point-in-a-circle.png
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
[Link](https://leetcode.com/problems/generate-random-point-in-a-circle/){:target="_blank"}

# 코드
```java
class Solution {

  private double radius;
  private double x_center;
  private double y_center;
  private Random random;

  public Solution(double radius, double x_center, double y_center) {
    this.radius = radius;
    this.x_center = x_center;
    this.y_center = y_center;
    this.random = new Random();
  }

  public double[] randPoint() {
    double x = this.getCoordinate(this.x_center);
    double y = this.getCoordinate(this.y_center);
    while (this.getDistanceAboutCenter(x, y) > this.radius * this.radius) {
      x = this.getCoordinate(this.x_center);
      y = this.getCoordinate(this.y_center);
    }
    return new double[] { x, y };
  }

  private double getDistanceAboutCenter(double x, double y) {
    double x_distance = this.x_center - x;
    double y_distance = this.y_center - y;
    return (x_distance * x_distance) + (y_distance * y_distance);
  }

  private double getCoordinate(double center) {
    return center - this.radius + (this.random.nextDouble() * 2 * this.radius);
  }

}

/**
 * Your Solution object will be instantiated and called as such:
 * Solution obj = new Solution(radius, x_center, y_center);
 * double[] param_1 = obj.randPoint();
 */
```

# 결과
[Link](https://leetcode.com/submissions/detail/693536721/){:target="_blank"}

# 설명
1. [x_center, y_center]의 위치에서 반지름이 radius인 원 내 임의 점을 생성하는 Solution 클래스를 완성하는 문제이다.
- 생성자인 Solution(double radius, double x_center, double y_center)은 객체를 초기화하는 역할을 수행한다.
- 메서드인 randPoint()는 [x_center, y_center]의 위치에서 반지름이 radius인 원 안과 둘레를 포함한 위치 내 임의 점의 위치를 [x, y] 형태의 배열로 반환한다.

2. 문제 풀이에 필요한 전역 변수를 정의한다.
- radius는 생성자를 통해 주입된 반지름의 길이를 저장하기 위한 변수이다.
- x_center는 생성자를 통해 주입된 원의 중심인 x축을 저장하기 위한 변수이다.
- y_center는 생성자를 통해 주입된 원의 중심인 y축을 저장하기 위한 변수이다.
- random은 임의 값을 반환하기 위한 변수이다.

3. 생성자인 Solution(double radius, double x_center, double y_center)을 완성한다.
- 생성자를 통해 주입된 radius, x_center, y_center를 각 전역 변수에 넣어준다.
- random은 java에서 임의 수를 반환하는 Random 객체를 초기화하여 넣어준다.

4. 메서드인 randPoint()를 정의한다.
- x와 y에 각 축의 중심인 x_center와 y_center를 5번에서 정의한 getCoordinate(double center) 메서드를 수행한 결과를 넣어준다.
- x와 y를 이용하여 원 밖을 벗어나는 경우, 다시 윗 단계를 수행하여 원 내에 존재할 때까지 반복을 수행한다.
- 원 내 존재하는 점의 위치인 x와 y를 배열로 생성하여 반환한다.

5. x축과 y축의 중심부 기준으로 임의 점을 생성하여 반환할 getCoordinate(double center) 메서드를 정의한다.
- center에서 radius를 뺀 값에 임의 0에서 1 사이의 수를 생성하여 radius의 2배 값을 곱해 더해준다.
  - x축인 경우, x축의 가장 좌측인 낮은 값의 위치에서 가장 우측인 높은 값 위치까지 임의 수를 생성하게 한다.
  - y축인 경우, y축의 가장 아래인 낮은 값의 위치에서 가장 위인 높은 값 위치까지 임의 수를 생성하게 한다.

6. 원 내 임의 점과 원 중심의 거리를 계산하는 getDistanceAboutCenter(double x, double y) 메서드를 정의한다.
- x_distance에 x_center와 x의 차이를, y_distance에 y_center와 y의 차이를 저장한다.
- x_distance와 y_distance의 각 제곱의 합을 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/object/solution/random/point/Solution.java){:target="_blank"}에서 확인 가능합니다.