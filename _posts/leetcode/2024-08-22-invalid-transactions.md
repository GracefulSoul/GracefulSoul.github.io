---
title: "Leetcode Java Invalid Transactions"
excerpt: "Leetcode Invalid Transactions Java"
last_modified_at: 2024-08-22T17:50:00
header:
  image: /assets/images/leetcode/invalid-transactions.png
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
[Link](https://leetcode.com/problems/invalid-transactions/){:target="_blank"}

# 코드
```java
class Solution {

  public List<String> invalidTransactions(String[] transactions) {
    Map<String, List<String[]>> map = new HashMap<>();
    for (String transaction : transactions) {
      String[] split = transaction.split(",");
      map.putIfAbsent(split[0], new ArrayList<>());
      map.get(split[0]).add(split);
    }
    List<String> result = new ArrayList<>();
    for (String transaction : transactions) {
      String[] split = transaction.split(",");
      if (Integer.parseInt(split[2]) > 1000) {
        result.add(transaction);
      } else {
        for (String[] curr : map.get(split[0])) {
          if (Math.abs(Integer.parseInt(split[1]) - Integer.parseInt(curr[1])) <= 60 && !split[3].equals(curr[3])) {
            result.add(transaction);
            break;
          }
        }
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/invalid-transactions/submissions/1364422756/){:target="_blank"}

# 설명
1. 이름, 시간, 금액, 도시의 순서의 값을 쉼표(",")단위로 구분한 값들이 저장된 transactions 내 아래의 조건을 하나라도 만족하는 유효하지 않는 거래들을 찾는 문제이다.
- 금액이 $1000를 초과하는 경우.
- 60분 이내에 같은 이름의 다른 도시에서 거래가 발생한 경우.

2. 문제 풀이에 필요한 변수를 정의한다.
- map은 transactions의 각 값을 이름 별 분리하여 저장한 변수로, transactions의 각 값의 이름에 대한 분리된 배열을 넣어준다.
- result는 유효하지 않는 거래를 저장할 변수로, ArrayList로 초기화한다.

3. transactions를 순차적으로 transaction에 넣어 아래를 반복한다.
- split에 transaction를 쉼표(",") 단위로 분리하여 넣어준다.
- 금액인 split[2]가 1000을 초과하는 경우, result에 transction을 넣어준다.
- 위의 경우가 아니라면 map의 split[0]인 도시에 해당하는 값을 꺼내 curr에 넣은 후 모든 값을 아래를 반복한다.
  - $split[1] - curr[1]$의 값이 60 이하인 다른 거래가 존재하면서 split[3]와 curr[3]의 값이 다른 도시인 경우, result에 transction을 넣고 반복을 중지한다.

4. 반복이 완료되면 유효하지 않은 거래가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/InvalidTransactions.java){:target="_blank"}에서 확인 가능합니다.