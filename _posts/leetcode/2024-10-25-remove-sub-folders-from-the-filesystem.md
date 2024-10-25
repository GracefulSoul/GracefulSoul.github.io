---
title: "Leetcode Java Remove Sub-Folders from the Filesystem"
excerpt: "Leetcode - 'Remove Sub-Folders from the Filesystem' 문제 Java 풀이"
last_modified_at: 2024-10-25T17:30:00
header:
  image: /assets/images/leetcode/remove-sub-folders-from-the-filesystem.png
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
[Link](https://leetcode.com/problems/remove-sub-folders-from-the-filesystem/){:target="_blank"}

# 코드
```java
class Solution {

  public List<String> removeSubfolders(String[] folder) {
    Arrays.sort(folder);
    List<String> result = new ArrayList<>();
    for (String path : folder) {
      if (result.isEmpty() || !path.startsWith(result.get(result.size() - 1) + "/")) {
        result.add(path);
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/remove-sub-folders-from-the-filesystem/submissions/1433207149/){:target="_blank"}

# 설명
1. folder 중에서 하위 폴더를 제외한 상위 폴더들을 찾는 문제이다.

2. folder를 사전 기준 오름차순으로 정렬해준다.

3. result는 결과를 넣을 변수로, ArrayList로 초기화한다.

4. folder의 각 값들을 순차적으로 path에 넣고 아래를 수행한다.
- 아래의 각 경우 중 하나라도 해당하면 result에 path를 넣어준다.
  - result가 비어있는 첫 수행인 경우, 사전적으로 가장 작은 폴더 경로이므로 추가한다.
  - path가 result에 마지막으로 들어간 값과 동일하게 시작되지 않는 하위 폴더가 아닌 경우.

5. 반복이 완료되면 결과가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RemoveSubFoldersFromTheFilesystem.java){:target="_blank"}에서 확인 가능합니다.