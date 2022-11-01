---
title: "Leetcode Java Random Pick with Blacklist"
excerpt: "Leetcode Random Pick with Blacklist Java"
last_modified_at: 2022-11-01T22:20:00
header:
  image: /assets/images/leetcode/random-pick-with-blacklist.png
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
[Link](https://leetcode.com/problems/random-pick-with-blacklist){:target="_blank"}

# 코드
```java
class Solution {

  private Random random;
  private Map<Integer, Integer> map;
  private int size;

  public Solution(int n, int[] blacklist) {
    this.random = new Random();
    this.map = new HashMap<Integer, Integer>();
    this.size = n - blacklist.length;
    for (int blacklistNum : blacklist) {
      if (blacklistNum >= this.size) {
        this.map.put(blacklistNum, -1);
      }
    }
    int index = n - 1;
    for (int blacklistNum : blacklist) {
      if (blacklistNum < this.size) {
        while (this.map.containsKey(index--)) {
        }
        this.map.put(blacklistNum, index + 1);
      }
    }
  }

  public int pick() {
    int num = this.random.nextInt(this.size);
    return this.map.getOrDefault(num, num);
  }

}

/**
 * Your Solution object will be instantiated and called as such:
 * Solution obj = new Solution(n, blacklist);
 * int param_1 = obj.pick();
 */
```

# 결과
[Link](https://leetcode.com/submissions/detail/834670031/){:target="_blank"}

# 설명
1. blacklist 내 값들을 제외한 [0, $n - 1$] 범위 내 값들을 동일한 확률로 반환하는 객체를 만드는 문제이다.
- 생성자인 Solution(int n, int[] blacklist)은 n과 blaclist를 이용하여 객체를 초기화한다.
- 메서드인 pick()은 [0, $n - 1$] 범위 내 값들 중 blacklist 외 값들을 동일한 확률로 반환하는 역할을 수행한다.
  - 일반적으로 blacklist의 반의어는 whitelist라고 한다.

2. 문제 풀이에 필요한 전역 변수를 정의한다.
- random은 객체 내 존재하는 값을 동일한 확률로 반환하기 위한 변수이다.
- map은 [0, $n - 1$] 범위 내 값들을 blacklist를 제외하고 값을 저장하기 위한 변수이다.
- size는 blacklist에 포함되지 않은 값들의 크기를 저장할 변수이다.

3. 생성자인 Solution(int n, int[] blacklist)을 완성한다.
- 문제 풀이에 필요한 전역 변수를 초기화한다.
  - random에 Random 객체를 초기화하여 넣어준다.
  - map은 key와 value로 넣기 위해 HashMap으로 초기화한다.
  - size는 blacklist를 제외한 값들의 길이를 구하기 위해 n에서 해당 길이를 빼서 저장한다.
- blacklist를 반복하여 size보다 큰 값이 key인 value에 -1을 넣어, blacklist에 포함되는 값임을 표시해준다.
- index는 [0, size] 범위에 포함되는 blacklist 값과 범위 외 whitelist 값을 key-value로 묶기 위한 값으로, 최대 숫자 범위인 $n - 1$로 초기화한다.
- blacklist의 모든 값들을 blacklistNum에 넣어 아래를 반복 수행한다.
  - blacklistNum이 size보다 작은 경우, [0, size] 범위 밖의 whitelist 값과 key-value로 연동하기 위해서 다음을 수행하고 그렇지 않으면 반복을 계속 수행한다.
  - map에 index가 key인 값이 존재하면 index를 감소시켜 blacklist에 포함되지 않은 값을 찾는다.
  - 위의 반복이 완료되면 blacklistNum이 key인 value에 $index + 1$인 whitelist 값을 넣어준다.

6. 메서드인 pick()을 완성한다.
- num에 [0, size] 내 임의 정수를 반환시킨다.
- map에서 num번째 값이 존재하는 경우 blacklist 값과 위치를 바꾼 whitelist 값을 가져오고, 존재하지 않는 경우 num인 whitelist 값을 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/object/solution/random/pick/blacklist/Solution.java){:target="_blank"}에서 확인 가능합니다.