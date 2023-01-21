---
title: "Leetcode Java Subdomain Visit Count"
excerpt: "Leetcode Subdomain Visit Count Java"
last_modified_at: 2023-01-21T11:30:00
header:
  image: /assets/images/leetcode/subdomain-visit-count.png
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
[Link](https://leetcode.com/problems/subdomain-visit-count){:target="_blank"}

# 코드
```java
class Solution {

  public List<String> subdomainVisits(String[] cpdomains) {
    Map<String, Integer> map = new HashMap<>();
    for (String cpdomain : cpdomains) {
      String[] split = cpdomain.split(" ");
      this.saveCpdomains(map, split[1], Integer.valueOf(split[0]));
    }
    List<String> result = new ArrayList<>();
    for (Map.Entry<String, Integer> entry : map.entrySet()) {
      result.add(entry.getValue() + " " + entry.getKey());
    }
    return result;
  }

  private void saveCpdomains(Map<String, Integer> map, String domain, int time) {
    map.put(domain, map.getOrDefault(domain, 0) + time);
    int index = domain.indexOf('.');
    if (index != -1) {
      this.saveCpdomains(map, domain.substring(index + 1, domain.length()), time);
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/subdomain-visit-count/submissions/882143428/){:target="_blank"}

# 설명
1. 방문 횟수와 도메인이 이어진 Count-Paired Domain이 저장된 cpdomains의 서브 도메인 별 방문 횟수를 계산하여 동일한 형태로 반환하는 문제이다.

2. map은 서브 도메인 별 방문 횟수를 계산하기 위한 변수로, cpdomains의 모든 값들을 cpdomain으로 3번에서 정의한 saveCpdomains(Map<String, Integer> map, String domain, int time) 메서드를 수행하여 값을 채워준다.

3. 서브 도메인 별 방문 횟수를 저장하기 위한 saveCpdomains(Map<String, Integer> map, String domain, int time) 메서드를 정의한다.
- map의 domain이 키인 값에 time을 더해서 넣어준다.
- index에 domain 내 '.'이 들어간 위치 값을 넣어준다.
- index가 -1이 아닌 서브 도메인이 있는 경우, domain의 서브 도메인을 이용하여 재귀 호출을 수행한다.

4. 결과를 저장하기 위한 result를 정의하여 map에 저장된 서브 도메인 별 방문 횟수를 Count-Paired Domain으로 저장 후 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SubdomainVisitCount.java){:target="_blank"}에서 확인 가능합니다.