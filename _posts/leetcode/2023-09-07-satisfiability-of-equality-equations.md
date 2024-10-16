---
title: "Leetcode Java Satisfiability of Equality Equations"
excerpt: "Leetcode Satisfiability of Equality Equations Java"
last_modified_at: 2023-09-07T18:40:00
header:
  image: /assets/images/leetcode/satisfiability-of-equality-equations.png
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
[Link](https://leetcode.com/problems/satisfiability-of-equality-equations){:target="_blank"}

# 코드
```java
class Solution {

  public boolean equationsPossible(String[] equations) {
    int[] parent = new int[26];
    for (int i = 0; i < 26; i++) {
      parent[i] = i;
    }
    for (String equation : equations) {
      if (equation.charAt(1) == '=') {
        parent[this.find(parent, equation.charAt(0) - 'a')] = this.find(parent, equation.charAt(3) - 'a');
      }
    }
    for (String equation : equations) {
      if (equation.charAt(1) == '!' && this.find(parent, equation.charAt(0) - 'a') == this.find(parent, equation.charAt(3) - 'a')) {
        return false;
      }
    }
    return true;
  }

  private int find(int[] parent, int i) {
    if (parent[i] == i) {
      return i;
    } else {
      return parent[i] = this.find(parent, parent[i]);
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/satisfiability-of-equality-equations/submissions/1042925276/){:target="_blank"}

# 설명
1. 아래의 규칙을 만족하는 방정식들이 담긴 equations에 동일한 숫자를 대입하여 만족할 수 있는지 검증하는 문제이다.
- equations[i] = x<sub>i</sub>==y<sub>i</sub> 혹은 equations[i] = x<sub>i</sub>!=y<sub>i</sub>의 4 글자로 이루어져있다.
- x와 y의 자리에는 영어 소문자 임의 문자가 들어갈 수 있다.

2. parent는 값을 유추하여 넣을 변수로, 영문자의 수인 각 위치에 위치 값을 임시로 넣어 초기화한다.

3. Union Find 방식으로 값을 탐색하기 위한 find(int[] parent, int i) 메서드를 정의한다.
- parent[i]의 값과 i가 동일한 경우, i를 반환한다.
- 위의 경우가 아니라면 parent[i]의 값과 parent와 parent[i]를 이용해 재귀 호출한 결과가 동일한지 여부를 반환한다.

4. equations의 모든 값을 equation으로 아래를 반복한다.
- equation의 두 번째 문자가 '='인 동등 연산의 경우, 3번에서 정의한 find 메서드를 활용하여 parent내 equation의 첫 번째 문자로 수행한 위치에 equation의 네 번째 문자로 수행한 결과를 넣어 값을 매칭시킨다.

5. equations의 모든 값을 equation으로 아래를 반복한다.
- 아래의 경우를 모두 만족하면, 동등 연산을 만족하는 경우이므로 false를 주어진 문제의 결과로 반환한다.
  - equation의 두 번째 문자가 '!'인 부등 연산인 경우.
  - 3번에서 정의한 find 메서드를 활용하여 equation의 첫 번째 문자로 수행한 결과와 equation의 네 번째 문자로 수행한 결과가 동일한 경우.

6. 반복이 완료되면 모든 연산을 만족하였으므로 true를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SatisfiabilityOfEqualityEquations.java){:target="_blank"}에서 확인 가능합니다.