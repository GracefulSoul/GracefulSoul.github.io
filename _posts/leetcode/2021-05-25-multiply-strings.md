---
title: "Leetcode Java Multiply Strings"
excerpt: "Leetcode - 'Multiply Strings' 문제 Java 풀이"
last_modified_at: 2021-05-25T18:00:00
header:
  image: /assets/images/leetcode/multiply-strings.png
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
[Link](https://leetcode.com/problems/multiply-strings/){:target="_blank"}

# 코드
```java
class Solution {

  public String multiply(String num1, String num2) {
    StringBuilder sb = new StringBuilder();
    for (int num : this.getNumberArray(num1, num2)) {
      if (sb.length() != 0 || num != 0) {
        sb.append(num);
      }
    }
    return sb.length() == 0 ? "0" : sb.toString();
  }
  
  private int[] getNumberArray(String num1, String num2) {
    int[] arr = new int[num1.length() + num2.length()];
    for (int i = num1.length() - 1; i >= 0; i--) {
      for (int j = num2.length() - 1; j >= 0; j--) {
        int sum = ((num1.charAt(i) - '0') * (num2.charAt(j) - '0')) + arr[i + j + 1];
        arr[i + j] += sum / 10;
        arr[i + j + 1] = sum % 10;
      }
    }
    return arr;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/497987443/){:target="_blank"}

# 설명
1. 주어진 문자열 num1과 num2의 길이의 합만큼 int 배열을 정의하여, 각 숫자의 곱의 숫자열을 저장할 변수 arr을 정의한다.
- $1\times1=1$, $9\times9=81$이므로 두 문자열의 곱의 최대 자릿수는 각 문자열의 길이의 합보다 같거나 작다.

2. 주어진 문자열 num1과 num2를 배열을 이용하여 각 숫자 별 곱을 구한다.
- 각 문자열을 반대로 반복하여 숫자의 곱을 구하고, 몫이 저장되는 $i + j + 1$의 자리의 숫자를 가져와 합쳐 변수 sum을 정의한다.
- 변수 sum의 몫인 $\frac{sum}{10}$을 배열 arr의 $i + j$에 더한다.
- 변수 sum의 나머지인 $sum\mod10$을 배열 arr의 $i + j + 1$에 주입한다.

3. 반복문을 통해 arr 배열의 값을 StringBuilder에 저장하여, 두 문자열의 곱을 하나의 문자열로 저장하여 주어진 문제의 결과로 반환한다.
- 동적 문자열의 생성시, 효율적인 메모리 사용을 위해 [StringBuilder](https://docs.oracle.com/javase/tutorial/java/data/buffers.html){:target="_blank"}를 사용한다.
- 정수는 항상 0이 아닌 숫자로 시작하므로, 만일 첫 문자열에 0이 들어가는 경우를 제외하고 지속적으로 append를 하여 숫자열을 완성한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MultiplyStrings.java){:target="_blank"}에서 확인 가능합니다.