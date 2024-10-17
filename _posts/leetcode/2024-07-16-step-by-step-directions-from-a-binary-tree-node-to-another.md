---
title: "Leetcode Java Step-By-Step Directions From a Binary Tree Node to Another"
excerpt: "Leetcode Medium - 'Step-By-Step Directions From a Binary Tree Node to Another' 문제 Java 풀이"
last_modified_at: 2024-07-16T18:30:00
header:
  image: /assets/images/leetcode/step-by-step-directions-from-a-binary-tree-node-to-another.png
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
[Link](https://leetcode.com/problems/step-by-step-directions-from-a-binary-tree-node-to-another/){:target="_blank"}

# 코드
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {

  public String getDirections(TreeNode root, int startValue, int destValue) {
    StringBuilder start = new StringBuilder();
    StringBuilder dest = new StringBuilder();
    this.findPaths(root, startValue, start);
    this.findPaths(root, destValue, dest);
    int count = 0;
    for (int i = start.length(), j = dest.length(); i > 0 && j > 0 && start.charAt(i - 1) == dest.charAt(j - 1); i--, j--) {
      count++;
    }
    return "U".repeat(start.length() - count) + dest.reverse().substring(count).toString();
  }

  private boolean findPaths(TreeNode node, int value, StringBuilder sb) {
    if (node.val == value) {
      return true;
    } else if (node.left != null && this.findPaths(node.left, value, sb)) {
      sb.append("L");
    } else if (node.right != null && this.findPaths(node.right, value, sb)) {
      sb.append("R");
    }
    return sb.length() > 0;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/step-by-step-directions-from-a-binary-tree-node-to-another/submissions/1322757909/){:target="_blank"}

# 설명
1. [1, n] 값을 가진 n개의 이진 트리 노드 root와 시작 위치 startValue, 목표 위치 destValue를 이용하여 시작 노드에서 목표 노드까지 가장 짧은 경로로 이동하기 위한 아래의 명령어를 반환하는 문제이다.
- 'L'은 노드에서 왼쪽 자식 노드로 가는 것을 의미한다.
- 'R'은 노드에서 오른쪽 자식 노드로 가는 것을 의미한다.
- 'U'는 노드에서 부모 노드로 가는 것을 의미한다.

2. start와 dest는 순차적으로 root노드에서 각각 startValue와 destValue로 도착하기 위한 경로를 만들 변수로, 모두 동적 문자열 생성을 위한 StringBuilder로 초기화한다.

3. 3번의 findPaths(TreeNode node, int value, StringBuilder sb) 메서드에 root와 startValue, start 변수와 destValue, dest 변수를 넣어 각각 수행한다.

4. root 노드에서 각자 목표의 값으로 이동하기 위한 명령어 생성을 위한 findPaths(TreeNode node, int value, StringBuilder sb) 메서드를 초기화한다.
- node의 val 값이 value이 목표 지점인 경우, true를 반환한다.
- node의 left 노드가 null이 아니면서 해당 노드로 재귀 호출한 결과가 true이면 이동 가능하므로, sb에 'L' 문자를 이어준다.
- node의 right 노드가 null이 아니면서 해당 노드로 재귀 호출한 결과가 true이면 이동 가능하므로, sb에 'R' 문자를 이어준다.
- 위의 모든 경우가 아니라면, sb가 0 초과인 이동한 이력이 있는지 여부를 반환한다.

5. 위의 수행이 완료되면 count에 root에서 start와 dest가 만나는 depth를 계산하여 넣어준다.

6. 아래의 두 문자열을 합쳐 주어진 문제의 결과로 반환한다.
- startValue 위치에서는 root 방향으로 올라가야하므로, 'U' 문자를 start의 길이에서 count를 뺀 횟수만큼 반복한 문자열을 먼저 위치한다.
- destValue 위치에서는 startValue가 내려올 위치를 저장해야 하므로, 아래의 문자열을 뒤에 이어준다.
  - root 방향으로 올라가기 위한 방향인 'L'과 'R' 문자가 저장된 dest를 역순으로 변환한다.
  - startValue가 root로 이동하다 destValue로 내려가는 위치인 노드에서 count번 이동하므로, 위의 역순 변환된 문자열의 count 위치 이후의 문자들을 문자열로 만들어준다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/StepByStepDirectionsFromABinaryTreeNodeToAnother.java){:target="_blank"}에서 확인 가능합니다.