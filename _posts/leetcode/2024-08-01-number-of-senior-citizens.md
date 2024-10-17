---
title: "Leetcode Java Number of Senior Citizens"
excerpt: "Leetcode Easy - 'Number of Senior Citizens' 문제 Java 풀이"
last_modified_at: 2024-08-01T17:50:00
header:
  image: /assets/images/leetcode/number-of-senior-citizens.png
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
[Link](https://leetcode.com/problems/number-of-senior-citizens/){:target="_blank"}

# 코드
```java
class Solution {

  public int countSeniors(String[] details) {
    int result = 0;
    for (String detail : details) {
      char ten = detail.charAt(11);
      if (ten > '6' || (ten == '6' && detail.charAt(12) > '0')) {
        result++;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/number-of-senior-citizens/submissions/1340480448/){:target="_blank"}

# 설명
1. details의 승객 정보를 이용하여 60세 초과인 승객 수를 계산하는 문제이다.
- 승객 정보의 처음 10자리는 핸드폰 번호를 의미한다.
- 승객 정보의 다음 문자는 성별을 의미한다.
- 승객 정보의 다음 두 문자는 나이를 의미한다.
- 승객 정보의 마지막 두 문자는 좌석을 의미한다.

2. result는 60세 초과인 승객의 수를 계산할 변수로, 0으로 초기화한다.

3. details의 각 값을 차례대로 detail에 넣어 아래를 수행한다.
- ten은 10의 자리에 해당하는 값을 저장할 변수로, detail의 11번째 위치 문자를 넣어준다.
- ten이 '6' 초과인 70세 이상이거나 '6'이면서 1의 자리에 해당하는 detail의 12번째 위치 문자가 '0' 초과인 경우, result를 증가시켜준다.

4. 반복이 완료되면 계산된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/NumberOfSeniorCitizens.java){:target="_blank"}에서 확인 가능합니다.