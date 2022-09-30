---
title: "Leetcode Java Map Sum Pairs"
excerpt: "Leetcode Map Sum Pairs Java"
last_modified_at: 2022-09-30T20:50:00
header:
  image: /assets/images/leetcode/map-sum-pairs.png
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
[Link](https://leetcode.com/problems/map-sum-pairs){:target="_blank"}

# 코드
```java
class MapSum {

  private Map<String, Integer> map;
  private TrieNode root;

  public MapSum() {
    this.map = new HashMap<>();
    this.root = new TrieNode();
  }

  public void insert(String key, int val) {
    int diff = val - this.map.getOrDefault(key, 0);
    TrieNode curr = this.root;
    for (char c : key.toCharArray()) {
      int num = c - 'a';
      if (curr.children[num] == null) {
        curr.children[num] = new TrieNode();
      }
      curr = curr.children[num];
      curr.sum += diff;
    }
    this.map.put(key, val);
  }

  public int sum(String prefix) {
    TrieNode curr = this.root;
    for (char c : prefix.toCharArray()) {
      int num = c - 'a';
      if (curr.children[num] == null) {
        return 0;
      }
      curr = curr.children[num];
    }
    return curr.sum;
  }

}

class TrieNode {

  public int sum;
  public TrieNode[] children;

  public TrieNode() {
    this.sum = 0;
    this.children = new TrieNode[26];
  }

}

/**
 * Your MapSum object will be instantiated and called as such:
 * MapSum obj = new MapSum();
 * obj.insert(key,val);
 * int param_2 = obj.sum(prefix);
 */
```

# 결과
[Link](https://leetcode.com/submissions/detail/812008967/){:target="_blank"}

# 설명
1. 문자들을 입력받고, 임의 문자열이 주어지면 해당 문자열이 접두사인 문자들의 값을 모두 합한 값을 반환하는 객체를 만드는 문제이다.
- 생성자인 MapSum()는 객체를 초기화한다.
- 메서드인 insert(String key, int val)는 객체 내 key 값과 val 값을 저장한다. 단, 동일한 key가 주어지면 새로 주입된 val 값으로 덮어쓴다.
- 메서드인 sum(string prefix)은 prefix로 시작되는 key들을 찾아 val 값들을 더해 반환한다.

2. 문제 풀이에 필요한 TrieNode 클래스를 정의한다.
- sum은 해당 단어까지의 문자열이 접두사인 val 값의 합을 저장할 변수이다.
- children은 해당 단어까지의 문자열 이후의 문자열을 이어주기 위한 변수로, 객체 생성 시 다음 문자를 저장하기 위해 알파벳의 갯수인 26 크기의 TrieNode 배열로 초기화 한다.

3. 문제 풀이에 필요한 변수를 정의한다.
- map은 insert(String key, int val)로 주입된 key와 val을 저장할 변수이다.
- root는 Trie의 가장 최상위 노드를 저장하기 위한 변수이다.

4. 생성자인 MapSum()를 정의한다.
- map을 HashMap으로, root를 TrieNode로 초기화한다.

5. 메서드인 insert(String key, int val)를 정의한다.
- diff에 val 값과 map에서 key에 해당하는 값 혹은 값이 없으면 0을 뺀 값을 넣어준다.
- 현재 TrieNode를 의미하는 curr에 root를 넣어준다.
- key를 문자 배열로 변환하여 c에 각각 넣어 아래를 반복한다.
  - num에 문자 c의 알파벳 순서인 0(a) ~ 25(z)를 계산하여 넣어준다.
  - curr 내 children의 num번째 값이 null이면 새 TrieNode를 넣어 초기화해준다.
  - curr에 curr의 children의 num번째 TrieNode를 넣어 다음 문자로 이동한다.
  - curr의 sum에 diff를 더해 해당 문자열이 접두사인 값의 합을 증가시킨다.
- 반복이 완료되면 map의 key에 해당하는 값에 val을 넣어 저장한다.

6. 메서드인 sum(string prefix)을 정의한다.
- 현재 TrieNode를 의미하는 curr에 root를 넣어준다.
- key를 문자 배열로 변환하여 c에 각각 넣어 아래를 반복한다.
  - num에 문자 c의 알파벳 순서인 0(a) ~ 25(z)를 계산하여 넣어준다.
  - curr 내 children의 num번째 값이 null이면 해당 prefix에 해당하는 문자열이 없으므로, 0을 반환한다.
  - curr에 curr의 children의 num번째 TrieNode를 넣어 다음 문자로 이동한다.
- 반복이 완료되면 접두사 위치의 문자들 값의 합인 curr의 sum을 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MapSumPairs.java){:target="_blank"}에서 확인 가능합니다.