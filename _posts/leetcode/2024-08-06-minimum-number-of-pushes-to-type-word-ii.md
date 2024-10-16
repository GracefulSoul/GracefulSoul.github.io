---
title: "Leetcode Minimum Number of Pushes to Type Word II"
excerpt: "Leetcode Minimum Number of Pushes to Type Word II Java"
last_modified_at: 2024-08-06T18:10:00
header:
  image: /assets/images/leetcode/minimum-number-of-pushes-to-type-word-ii.png
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
[Link](https://leetcode.com/problems/minimum-number-of-pushes-to-type-word-ii/){:target="_blank"}

# 코드
```java
class Solution {

  public int minimumPushes(String word) {
    int[] counts = new int[26];
    for (char c : word.toCharArray()) {
      counts[c - 'a']++;
    }
    Arrays.sort(counts);
    int result = 0;
    for (int i = 25, multiplier = 1, count = 0; i >= 0 && counts[i] > 0; i--) {
      result += multiplier * counts[i];
      count++;
      if (count == 8) {
        multiplier++;
        count = 0;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-number-of-pushes-to-type-word-ii/submissions/1346378094/){:target="_blank"}

# 설명
1. 영문자로 이루어진 옛날 전화기 키패드를 이용하여 주어진 word를 입력하기 위한 횟수를 최소로 하기 위해 재배열하여 해당 횟수를 반환하는 문제이다.
- 일반적으로 영문 전화기 키패드는 아래와 같다.
- <table style="border: 2px; text-align : center">
    <tr>
      <td>1</td>
      <td>2 abc</td>
      <td>3 def</td>
    </tr>
    <tr>
      <td>4 ghi</td>
      <td>5 abc</td>
      <td>6 def</td>
    </tr>
    <tr>
      <td>7 pqrs</td>
      <td>8 tuv</td>
      <td>9 wxyz</td>
    </tr>
    <tr>
      <td>*</td>
      <td>0</td>
      <td>#</td>
    </tr>
  </table>

2. 문제 풀이에 필요한 변수를 정의한다.
- counts는 문자열의 갯수를 저장할 변수로, 26 크기의 정수 배열로 초기화하여 word 내 각 문자의 갯수를 계산하여 오름차순으로 정렬해준다.
- result는 결과를 저장할 변수로, 0으로 초기화한다.

3. 동일 버튼을 누르는 횟수를 계산할 multiplier는 1로, 문자열이 존재하는 버튼의 이동을 저장할 count는 0으로, i는 25부터 0 이상이면서 counts[i]의 갯수가 0 초과일 때 까지 아래를 반복한다.
- result에 $multiplier * counts[i]$인 푸시 횟수를 더해준다.
- count를 증가시켜 다음 버튼 위치로 이동시킨다.
- count가 8인 다시 처음 버튼으로 이동해야 하는 경우, multiplier를 증가시켜 버튼을 누르는 횟수의 가중치를 증가시키고 count를 0으로 초기화한다.

4. 반복이 완료되면 최소 푸시 횟수가 계산된 result를 주어진 문제의 결과로 반환한다.

# 해설
- 영문 전화기 키패드의 문자를 재배열 할 수 있으므로, 문자가 존재하는 2 ~ 9까지 버튼의 수인 8 기반으로 문자열을 재배치한다.
- 재배치는 한 번 눌러야 하는 위치에 많이 존재하는 문자를 순차적으로 넣어야 버튼을 누르는 횟수가 최소가 된다.
- 위를 바탕으로 8개 단위로 가중치를 둔 이유는, 각 숫자열 임의 위치에 순차적으로 앞의 한 번 눌러야 입력되는 문자에 넣고 다음 가중치에 다시 순차적으로 넣기 위함이다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumNumberOfPushesToTypeWordII.java){:target="_blank"}에서 확인 가능합니다.