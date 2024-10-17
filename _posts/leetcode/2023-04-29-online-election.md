---
title: "Leetcode Java Online Election"
excerpt: "Leetcode - 'Online Election' 문제 Java 풀이"
last_modified_at: 2023-04-29T09:30:00
header:
  image: /assets/images/leetcode/online-election.png
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
[Link](https://leetcode.com/problems/online-election){:target="_blank"}

# 코드
```java
class TopVotedCandidate {

  private int[] lead;
  private int[] times;

  public TopVotedCandidate(int[] persons, int[] times) {
    int length = persons.length;
    int[] votes = new int[length];
    this.lead = new int[length];
    this.times = times;
    int max = 0;
    for (int i = 0; i < length; i++) {
      int person = persons[i];
      votes[person]++;
      if (votes[person] >= max) {
        max = votes[person];
        this.lead[i] = person;
      } else {
        this.lead[i] = this.lead[i - 1];
      }
    }
  }

  public int q(int t) {
    int num = Arrays.binarySearch(this.times, t);
    if (num < 0) {
      num = -num - 2;
    }
    return this.lead[num];
  }

}

/**
 * Your TopVotedCandidate object will be instantiated and called as such:
 * TopVotedCandidate obj = new TopVotedCandidate(persons, times);
 * int param_1 = obj.q(t);
 */
```

# 결과
[Link](https://leetcode.com/problems/online-election/submissions/941341312/){:target="_blank"}

# 설명
1. 선거자와 시간을 입력하여 해당 시간에 승리하는 사람을 구하는 TopVotedCandidate 클래스를 완성하는 문제이다.
- 생성자인 TopVotedCandidate(int[] persons, int[] times)는 선거인과 시간을 초기화하는 역할을 수행한다.
- 메서드인 int q(int t)는 t시간에 가장 최고 득표한 사람을 반환하는 역할을 수행한다.

2. 문제 풀이에 필요한 전역 변수를 정의한다.
- lead는 각 시간 별 최고 득표하고 있는 사람을 저장하기 위한 변수이다.
- times는 주어진 시간을 저장하기 위한 변수이다.

3. 생성자인 TopVotedCandidate(int[] persons, int[] times)를 정의한다.
- 객체 초기화에 필요한 변수를 정의한다.
  - length는 persons의 길이를 저장하기 위한 변수이다.
  - votes는 선거자 별 투표 수를 계산하기 위한 변수로, length 크기의 정수 배열로 초기화한다.
  - lead에는 에는 length 크기의 정수 배열로, times에는 주어진 times를 넣어 초기화한다.
  - max는 최대 득표 수를 저장하기 위한 변수로, 0으로 초기화한다.
- 0부터 length 미만까지 i를 증가시키며 아래를 수행한다.
  - person에 persons의 i번째 선거자를 넣고, votes의 person번째 값을 증가시킨다.
  - votes의 person번째 값이 max보다 크거나 같으면 max에 해당 값을 넣고 lead의 i번째 값에 person을 넣어준다.
  - 위의 경우가 아니라면 lead에 이전까지 득표 수가 많았던 선거자를 넣어준다.

4. 메서드인 int q(int t)를 정의한다.
- num에 times에서 t에 해당하는 값 혹은 인접한 위치의 값을 찾아 넣어준다.
  - Arrays.binarySearch(int[] a, int key) 메서드는 배열 내 값이 없을 경우, 인접한 두 값 사이의 위치보다 하나 작은 값을 반환한다.
- num이 0보다 작은 경우, 위의 설명과 같으므로 num에 num을 양수로 전환하여 2를 뺀 값을 넣어준다.
- lead의 num번째 선거자를 찾아 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/OnlineElection.java){:target="_blank"}에서 확인 가능합니다.