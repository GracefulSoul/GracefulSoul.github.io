---
title: "Leetcode Java Number of Burgers with No Waste of Ingredients"
excerpt: "Leetcode - 'Number of Burgers with No Waste of Ingredients' 문제 Java 풀이"
last_modified_at: 2025-07-23T21:30:00
header:
  image: /assets/images/leetcode/number-of-burgers-with-no-waste-of-ingredients.png
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
[Link](https://leetcode.com/problems/number-of-burgers-with-no-waste-of-ingredients/){:target="_blank"}

# 코드
```java
class Solution {

  public List<Integer> numOfBurgers(int tomatoSlices, int cheeseSlices) {
    int doubleJumbo = tomatoSlices - (2 * cheeseSlices);
    int jumbo = doubleJumbo / 2;
    int small = cheeseSlices - jumbo;
    if (0 <= jumbo && doubleJumbo % 2 == 0 && 0 <= small) {
      return Arrays.asList(jumbo, small);
    } else {
      return new ArrayList<>();
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/number-of-burgers-with-no-waste-of-ingredients/submissions/1708460174/){:target="_blank"}

# 설명
1. 아래 조합의 햄버거를 남은 재료 없이 만들기 위한 조합을 [점보 버거 수, 스몰 버거 수]로 반환하는 문제이다.
- 점보 버거는 4개의 썰은 토마토와 1개의 썰은 치즈가 필요하다.
- 점보 버거는 2개의 썰은 토마토와 1개의 썰은 치즈가 필요하다.
- 남은 재료가 존재하는 경우, 빈 ArrayList를 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- doubleJumbo는 만들 수 있는 점보 버거 수의 두배를 저장한 변수로, $tomatoSlices - (2 \times cheeseSlices)$로 초기화한다.
- jumbo는 만들 수 있는 점보 버거 수를 저장한 변수로, $\frac{doubleJumbo}{2}$로 초기화한다.
- small은 만들 수 있는 스몰 버거 수를 저장한 변수로, $cheeseSlices - jumbo$로 초기화한다.

3. 아래 조건을 모두 부합하면 jumbo와 small을 순서대로 ArrayList로 넣어 주어진 문제의 결과로 반환한다.
- jumbo가 0보다 크거나 같은 음수가 아닌 경우.
- doubleJumbo가 짝수인 jumbo를 만들면서 남는 재료가 없는 경우.
- small이 0보다 크거나 같은 음수가 아닌 경우.

# 해설
- tomatoSlices는 점보 버거에 4개, 스몰 버거에 2개 사용되므로 $tomatoSlices = (4 \times jumbo) + (2 \times small)$로 표기한다.
- cheeseSlices는 점보 버거에 1개, 스몰 버거에 1개 사용되므로 $cheeseSlices = jumbo + small$로 표기한다.
- 위 값을 기반으로 $doubleJumbo = 2 \times jumbo = tomatoSlices - (2 \times cheeseSlices)$가 성립한다.
- 위를 기반으로 $jumbo = \frac{doubleJumbo}{2}$가 되며, $small = cheeseSlices - jumbo$가 성립한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/NumberOfBurgersWithNoWasteOfIngredients.java){:target="_blank"}에서 확인 가능합니다.