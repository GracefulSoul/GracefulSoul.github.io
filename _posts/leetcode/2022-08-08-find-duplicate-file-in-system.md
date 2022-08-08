---
title: "Leetcode Java Find Duplicate File in System"
excerpt: "Leetcode Find Duplicate File in System Java"
last_modified_at: 2022-08-08T09:00:00
header:
  image: /assets/images/leetcode/find-duplicate-file-in-system.png
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
[Link](https://leetcode.com/problems/find-duplicate-file-in-system/){:target="_blank"}

# 코드
```java
class Solution {

  public List<List<String>> findDuplicate(String[] paths) {
    Map<String, List<String>> map = new HashMap<>();
    for (String path : paths) {
      String[] splits = path.split("\\s");
      for (int idx = 1; idx < splits.length; idx++) {
        String[] filePath = splits[idx].split("\\(");
        String content = filePath[1].substring(0, filePath[1].length() - 1);
        if (!map.containsKey(content)) {
          map.put(content, new ArrayList<>());
        }
        map.get(content).add(new StringBuilder(splits[0]).append("/").append(filePath[0]).toString());
      }
    }
    List<List<String>> result = new ArrayList<>();
    for (List<String> files : map.values()) {
      if (files.size() > 1) {
        result.add(files);
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/767970590/){:target="_blank"}

# 설명
1. 파일 위치가 담긴 paths에서 동일한 내용이 존재하는 파일들을 그룹지어 반환하는 문제이다.

2. 동일한 내용이 담긴 파일들을 넣을 map을 정의한다.

3. paths의 모든 값들을 반복하여 아래를 수행한다.
- splits에 path를 공백(" ") 기준으로 문자열을 분리해서 배열로 넣어준다.
- 1부터 splits의 길이 미만까지 idx를 증가시키며 아래를 반복한다.
  - filePath에 splits의 idx번째 값에서 소괄화의 시작 문자("(") 기준으로 문자열을 분리해서 배열로 넣어준다.
  - content에 filePath의 첫 번째인 텍스트 내용의 시작부터 끝까지 넣어준다.
  - map에 content가 존재하지 않으면, 신규 ArrayList를 생성하여 넣어준다.
  - map의 content에 대한 배열을 가져와 splits[0]인 디렉토리 위치에 filePath[0]인 파일 이름을 구분자("//")로 합친 문자열을 넣어준다.

4. 결과를 넣을 result를 ArrayList로 초기화 하고, map의 모든 값들을 반복하여 하나라도 값이 존재하는 파일 그룹들을 result에 넣어준다.

5. 위의 반복이 완료되면 그룹화하여 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindDuplicateFileInSystem.java){:target="_blank"}에서 확인 가능합니다.