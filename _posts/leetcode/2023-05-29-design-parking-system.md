---
title: "Leetcode Java Design Parking System"
excerpt: "Leetcode - 'Design Parking System' 문제 Java 풀이"
last_modified_at: 2023-05-29T14:45:00
header:
  image: /assets/images/leetcode/design-parking-system.png
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
[Link](https://leetcode.com/problems/design-parking-system){:target="_blank"}

# 코드
```java
class ParkingSystem {

  private int[] count;

  public ParkingSystem(int big, int medium, int small) {
    this.count = new int[] { big, medium, small };
  }

  public boolean addCar(int carType) {
    return this.count[carType - 1]-- > 0;
  }

}

/**
 * Your ParkingSystem object will be instantiated and called as such:
 * ParkingSystem obj = new ParkingSystem(big, medium, small);
 * boolean param_1 = obj.addCar(carType);
 */
```

# 결과
[Link](https://leetcode.com/problems/design-parking-system/submissions/959369833/){:target="_blank"}

# 설명
1. 각 차의 크기 별 주차할 수 있는 공간을 관리하는 ParkingSystem 객체를 정의하는 문제이다.
- 생성자인 ParkingSystem(int big, int medium, int small)은 big, medium, small의 주차 대수를 이용하여 객체를 초기화한다.
- 메서드인 addCar(int carType)는 carType별 주차 가능 여부를 관리하는 메서드로, big은 1을 medium은 2를 small은 3을 의미한다.

2. 주차 공간을 관리하기 위한 전역 변수를 정의한다.
- count는 각 차량의 크기 별 주차 가능 대수를 저장할 변수이다.

3. 생성자인 ParkingSystem(int big, int medium, int small)를 완성한다.
- count에 [big, medium, small] 순으로 주차 가능 공간을 저장한다.

4. 메서드인 addCar(int carType)를 완성한다.
- count의 $carType - 1$번째 값을 감소시키고, 주차가 가능한지 여부인 해당 값이 0보다 큰지 검증한 결과를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DesignParkingSystem.java){:target="_blank"}에서 확인 가능합니다.