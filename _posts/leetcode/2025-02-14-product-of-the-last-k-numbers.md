---
title: "Leetcode Java Product of the Last K Numbers"
excerpt: "Leetcode - 'Product of the Last K Numbers' 문제 Java 풀이"
last_modified_at: 2025-02-14T18:50:00
header:
  image: /assets/images/leetcode/product-of-the-last-k-numbers.png
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
[Link](https://leetcode.com/problems/product-of-the-last-k-numbers/){:target="_blank"}

# 코드
```java
class ProductOfNumbers {

  private List<Integer> list;
  private int product;

  public ProductOfNumbers() {
    this.list = new ArrayList<>();
    this.product = 1;
  }

  public void add(int num) {
    if (num != 0) {
      this.product *= num;
      this.list.add(product);
    } else {
      this.list.clear();
      this.product = 1;
    }
  }

  public int getProduct(int k) {
    int size = this.list.size();
    if (size < k) {
      return 0;
    } else {
      int num = this.list.get(size - 1);
      if (size == k) {
        return num;
      } else {
        return num / this.list.get(size - 1 - k);
      }
    }
  }

}

/**
 * Your ProductOfNumbers object will be instantiated and called as such:
 * ProductOfNumbers obj = new ProductOfNumbers();
 * obj.add(num);
 * int param_2 = obj.getProduct(k);
 */
```

# 결과
[Link](https://leetcode.com/problems/product-of-the-last-k-numbers/submissions/1542739985/){:target="_blank"}

# 설명
1. 아래 기능을 수행하는 객체를 만드는 문제이다.
- 생성자인 ProductOfNumbers()는 객체를 초기화하는 역할을 수행한다.
- 메서드인 add(int num)는 객체에 num을 이어 넣어준다.
- 메서드인 getProduct(int k)는 마지막 k개 값을 곱한 결과를 반환한다.

2. 수행에 필요한 전역 변수를 정의한다.
- list는 add 메서드를 통해 입력된 숫자를 저장할 변수이다.
- product는 입력된 숫자들의 곱을 저장할 변수이다.

3. 생성자인 ProductOfNumbers()를 정의한다.
- list를 ArrayList로, product를 1로 초기화한다.

4. 메서드인 add(int num)를 정의한다.
- num이 0이 아닌 경우, product에 num을 곱한 후 list에 product를 넣어 저장한다.
- num이 0이어서 product의 이전 값의 곱이 0이 되는 경우, list를 초기화하고 product를 1로 초기화한다.

5. 메서드인 getProduct(int k)를 정의한다.
- size에 list의 길이를 넣어준다.
- size가 k 미만인 경우, k개의 곱을 계산할 수 없으므로 0을 반환한다.
- 위의 경우가 아니라면, 아래를 수행한다.
  - num에 list의 마지막 값을 넣어준다.
  - size가 k인 기존 값을 모두 곱하는 경우, num을 반환한다.
  - 위의 경우가 아니라면 num에 list 내 $size - 1 - k$ 위치인 k개 이전까지 곱한 값을 가져와 나눈 값을 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ProductOfTheLastKNumbers.java){:target="_blank"}에서 확인 가능합니다.