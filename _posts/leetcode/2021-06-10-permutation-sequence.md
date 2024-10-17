---
title: "Leetcode Java Permutation Sequence"
excerpt: "Leetcode - 'Permutation Sequence' 문제 Java 풀이"
last_modified_at: 2021-06-10T12:20:00
header:
  image: /assets/images/leetcode/permutation-sequence.png
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
[Link](https://leetcode.com/problems/permutation-sequence/){:target="_blank"}

# 코드
```java
class Solution {

  private List<Integer> nums = new ArrayList<>();
  private int factorial = 1;

  public String getPermutation(int n, int k) {
    this.initVariable(n);
    StringBuilder sb = new StringBuilder();
    for (int i = 0, j = k - 1; i < n; i++) {
      this.factorial /= (n - i);
      int index = (j / this.factorial);
      sb.append(this.nums.remove(index));
      j -= index * this.factorial;
    }
    return sb.toString();
  }

  private void initVariable(int n) {
    for (int idx = 1; idx <= n; idx++) {
      this.factorial *= idx;
      this.nums.add(idx);
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/505230381/){:target="_blank"}

# 설명
1. 주어진 정수 n을 이용하여 1부터 n까지의 연속된 숫자 배열의 조합을 순차적으로 생성할 때, k번째 숫자 조합을 구하는 문제이다.

2. 주어진 문제를 위해 각 숫자를 저장한 컬렉션 nums와 n!의 결과를 저장할 factorial 변수를 선언한다.
- factorial을 구하는 이유는, 일련된 숫자의 조합을 구하는 경우의 수가 $n!$개 나오기 때문이다.
- 예를 들어 n이 3일 경우, $3! = 1 \times 2 \times 3 = 6$이고 조합은 [123, 132, 213, 231, 312, 321]의 6가지 조합이 나오게 된다.
- 위의 경우 k가 3인 경우, 3번 째 조합인 213이 주어진 문제의 결과이다.

3. 문제의 시작에 factorial과 nums를 초기화한다.
- 전역 변수로 선언 한 이유는, 해당 값들을 주입하고 모두 활용하여 문제의 종료에는 초기 값으로 설정되기 때문이다.
- nums는 빈 ArrayList, factorial은 1로 문제가 종료되기 때문에 반복된 변수 선언보다, 전역변수로 활용하는 것이 효율적이기 때문이다.

4. 주어진 문제의 결과는 String으로, 해당 숫자열을 동적인 문자열을 생성하기 위해 StringBuilder인 변수 sb를 선언한다.
- 동적 문자열의 생성시, 효율적인 메모리 사용을 위해 [StringBuilder](https://docs.oracle.com/javase/tutorial/java/data/buffers.html){:target="_blank"}를 사용한다.

5. i는 0 부터 각 자릿수만큼 반복하며, j는 $k - 1$을 주입하여 k번째 숫자의 조합을 생성한다.
- 각 자릿수의 경우의 수는 (n - i)이므로, $\frac{factorial}{n - 1}$을 factorial에 주입한다.
- 배열 nums의 $\frac{j}{factorial}$번째 index 값을 꺼내와 sb에 이어쓴다.
  - $\frac{j}{factorial}$번째 index 값을 가져오는 이유는, 2번의 경우와 같다.
  - nums의 특정 자릿수의 값을 꺼내오기 위해 remove 메서드를 호출하였는데, 이는 해당 자리의 값을 꺼내오므로 이후 자리부터 index가 당겨지게 된다.
  - 예를 들어, 길이가 3인 nums의 값이 [1, 2, 3]인 경우 nums.remove(1)을 함으로써 길이가 2인 nums가 되며 값이 [1, 3]가 된다.
- 특정 자릿수의 값이 구해지면, j에 $index \times factorial$의 값을 빼준다.
  - 해당 이유도 2번의 경우와 같으므로, 자릿수가 구해지면 해당 자릿수 이후의 경우의 수가 넘어가지 않기 위해서이다.
  - 예를 들면 2번의 예제에서 첫 자리가 1이 나온 경우, 3번째 이후 값은 의미가 없으므로 범위를 좁히기 위해서이다.

6. 반복이 종료되면 주어진 변수 n을 이용하여 1부터 n까지 연속된 숫자의 k번째 조합을 저장한 sb를 String으로 변환하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PermutationSequence.java){:target="_blank"}에서 확인 가능합니다.