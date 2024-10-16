---
title: "Leetcode Java Encode and Decode TinyURL"
excerpt: "Leetcode Encode and Decode TinyURL Java"
last_modified_at: 2022-06-17T19:00:00
header:
  image: /assets/images/leetcode/encode-and-decode-tinyurl.png
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
[Link](https://leetcode.com/problems/encode-and-decode-tinyurl/){:target="_blank"}

# 코드
```java
class Codec {

  private Map<Integer, String> map = new HashMap<>();
  private static final String URL = "http://tinyurl.com/";

  // Encodes a URL to a shortened URL.
  public String encode(String longUrl) {
    int key = longUrl.hashCode();
    this.map.put(key, longUrl);
    return URL.concat(String.valueOf(key));
  }

  // Decodes a shortened URL to its original URL.
  public String decode(String shortUrl) {
    return this.map.get(Integer.parseInt(shortUrl.replace(URL, "")));
  }

}

// Your Codec object will be instantiated and called as such:
// Codec codec = new Codec();
// codec.decode(codec.encode(url));
```

# 결과
[Link](https://leetcode.com/submissions/detail/724327017/){:target="_blank"}

# 설명
1. URL을 임의 해시값을 사용하여 아래와 같이 암복호화하는 Codec 클래스를 완성하는 문제이다.
- "https://leetcode.com/problems/design-tinyurl"의 url이 주어지면 "http://tinyurl.com/4e9iAk"와 같이 짧은 url을 반환하고, 해당 url을 호출하면 원본 url로 호출이 수행된다.

2. 문제 풀이에 필요한 변수를 정의한다.
- map은 hash값을 이용하여 원본 url을 저장하기 위한 변수로, HashMap으로 초기화한다.
- URL은 예제와 같은 도메인을 저장할 변수로, "http://tinyurl.com/"로 초기화한다.

3. 메서드인 encode(String longUrl)를 완성한다.
- longUrl의 해시코드를 key로 정의하고, map 내 key에 해당하는 값을 longUrl로 넣어준다.
- URL에 key를 이어서 짧은 url을 만들어 반환한다.

4. 메서드인 decode(String shortUrl)를 완성한다.
- shortUrl에서 URL부분을 제거하고 map에서 해시코드에 해당하는 값을 꺼내 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/EncodeAndDecodeTinyURL.java){:target="_blank"}에서 확인 가능합니다.