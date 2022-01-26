---
title: "Leetcode Java Design Twitter"
excerpt: "Leetcode Design Twitter Java 풀이"
last_modified_at: 2022-01-26T13:00:00
header:
  image: /assets/images/leetcode/design-twitter.png
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
[Link](https://leetcode.com/problems/design-twitter/){:target="_blank"}

# 코드
```java
class Twitter {

  private List<Integer[]> posts;
  private Map<Integer, Set<Integer>> relation;

  public Twitter() {
    this.posts = new ArrayList<>();
    this.relation = new HashMap<>();
  }

  public void postTweet(int userId, int tweetId) {
    this.posts.add(new Integer[] { userId, tweetId });
  }

  public List<Integer> getNewsFeed(int userId) {
    List<Integer> newsFeed = new ArrayList<>();
    for (int idx = this.posts.size() - 1; idx >= 0 && newsFeed.size() < 10; idx--) {
      Integer[] post = this.posts.get(idx);
      Set<Integer> followees = this.relation.get(userId);
      if (post[0] == userId || (followees != null && followees.contains(post[0]))) {
        newsFeed.add(post[1]);
      }
    }
    return newsFeed;
  }

  public void follow(int followerId, int followeeId) {
    Set<Integer> followees = this.relation.get(followerId);
    if (followees == null) {
      followees = new HashSet<>();
    }
    followees.add(followeeId);
    this.relation.put(followerId, followees);
  }

  public void unfollow(int followerId, int followeeId) {
    Set<Integer> followees = this.relation.get(followerId);
    if (followees != null) {
      followees.remove(followeeId);
    }
  }

}

/**
 * Your Twitter object will be instantiated and called as such:
 * Twitter obj = new Twitter();
 * obj.postTweet(userId,tweetId);
 * List<Integer> param_2 = obj.getNewsFeed(userId);
 * obj.follow(followerId,followeeId);
 * obj.unfollow(followerId,followeeId);
 */
```

# 결과
[Link](https://leetcode.com/submissions/detail/627990146/){:target="_blank"}

# 설명
1. 사용자가 트윗을 게시하고, 다른 사용자를 팔로우 혹은 언팔로우 할 수 있으며, 최근 10개의 사용자의 뉴스 피드를 볼 수 있는 간단한 Twitter를 만드는 문제이다.
- 생성자인 Twitter()는 Twitter 객체를 초기화 시키는 역할을 한다.
- 메서드인 postTweet(int userId, int tweetId)은 게시한 user의 id인 userId와 고유한 새 tweet의 id인 tweetId를 엮어주는 역할을 한다.
- 메서드인 getNewsFeed(int userId)는 news feed를 검색하는 userId를 이용하여 해당 user가 follow한 사용자들의 최근 10개 news feed를 가져오는 역할을 한다.
- 메서드인 follow(int followerId, int followeeId)는 follow하는 userId와 follow받는 userId를 연결하는 역할이다.
- 메서드인 unfollow(int followerId, int followeeId)는 위의 follow(int followerId, int followeeId)와 반대로, follow한 연결 관계를 삭제하는 역할이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- posts는 userId와 tweetId를 엮어 저장할 post들을 저장할 List이다.
- relation은 user가 follow하는 계정들의 userId를 저장하기 위한 Map이다.

3. 생성자인 Twitter()를 완성한다.
- posts에 새 ArrayList를 넣어 초기화 시켜준다.
- relation에 새 HashMap을 넣어 초기화 시켜준다.

4. 메서드인 postTweet(int userId, int tweetId)을 완성한다.
- posts에 userId와 tweetId를 엮어 정수 배열로 넣어준다.

5. 메서드인 getNewsFeed(int userId)를 완성한다.
- 최근 10개의 newsFeed를 넣을 List인 newsFeed를 정의한다.
- posts를 역순으로 newsFeed가 10개가 되거나 idx가 0 이하가 될 때 까지 탐색하며 newsFeed를 넣어준다.
  - posts의 idx번째 배열을 꺼내 post로 정의한다.
  - relation에서 userId의 follower 목록을 가져와 followees에 넣어준다.
  - post의 첫 번째 값이 userId이거나 followees가 존재하며 followees에 post의 첫 번째 값이 포함하는 경우 자기 자신의 newsFeed거나 follower의 newsFeed이므로, newsFeed에 post의 두 번째 값인 tweetId를 넣어주고 반복을 계속 수행한다.
- 반복이 완료되면 newsFeed를 반환한다.

6. 메서드인 follow(int followerId, int followeeId)를 완성한다.
- relation의 followerId에 해당하는 값을 가져와 followees로 정의한다.
- followees가 null인 경우 기존 follow하는 유저들이 없었다는 의미이므로, followees에 새 HashSet을 넣어준다.
- followees에 followeeId를 넣어주고, relation의 followerId에 해당 하는 값에 followees를 넣어준다.

7. 메서드인 unfollow(int followerId, int followeeId)를 완성한다.
- relation의 followerId에 해당하는 값을 가져와 followees로 정의한다.
- followees가 null이 아닌 경우 기존 follow하는 유저들이 있다는 의미이므로, folloewees에 followeeId를 삭제한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DesignTwitter.java){:target="_blank"}에서 확인 가능합니다.