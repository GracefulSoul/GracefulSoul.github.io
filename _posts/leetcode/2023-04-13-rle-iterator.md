---
title: "Leetcode Java RLE Iterator"
excerpt: "Leetcode RLE Iterator Java"
last_modified_at: 2023-04-13T20:30:00
header:
  image: /assets/images/leetcode/rle-iterator.png
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
[Link](https://leetcode.com/problems/rle-iterator){:target="_blank"}

# 코드
```java
class RLEIterator {

  private int[] encoding;
  private int index;

  public RLEIterator(int[] encoding) {
    this.encoding = encoding;
    this.index = 0;
  }

  public int next(int n) {
    while (this.index < this.encoding.length) {
      if (n > this.encoding[this.index]) {
        n -= this.encoding[this.index];
        this.index += 2;
      } else {
        this.encoding[this.index] -= n;
        return this.encoding[this.index + 1];
      }
    }
    return -1;
  }

}

/**
 * Your RLEIterator object will be instantiated and called as such:
 * RLEIterator obj = new RLEIterator(encoding);
 * int param_1 = obj.next(n);
 */
```

# 결과
[Link](https://leetcode.com/problems/rle-iterator/submissions/933030339/){:target="_blank"}

# 설명
1. i번째 위치에 반복되는 횟수와 $i + 1$번째 위치에 반복되는 숫자를 연속해서 RLE(run-length encoding)로 인코딩된 값을 이용하여 앞의 값들을 제거하고 남은 값들을 반환하는 RLEIterator 클래스를 구현하는 문제이다.
- 생성자인 RLEIterator(int[] encoding)는 encoding 배열의 값을 이용하여 객체를 초기화한다.
- 메서드인 next(int n)는 RLE로 인코딩된 배열을 숫자로 변환하여 앞 n개의 요소를 제거한 값을 저장 후 배열의 시작 값을 반환한다. 단, 반환할 값이 없는 경우 -1을 반환한다.

2. RLE로 인코딩에 사용할 전역 변수를 정의한다.
- encoding은 RLE 인코딩으로 변환된 값을 저장할 변수이다.
- index는 encoding을 복호화 하여 제거되지 않은 값의 시작 위치를 저장할 변수이다.

3. 생성자인 RLEIterator(int[] encoded)를 정의한다.
- encoding에 주어진 encoding을 넣어주고 index를 0으로 초기화한다.

4. 메서드인 next(int n)를 정의한다.
- index가 encoding의 길이 미만이 될 때까지 아래를 반복한다.
  - n이 encoding의 index번째 값보다 큰 경우 해당 값을 모두 소모하므로, n에 앞의 값을 빼주고 index를 2 증가시켜 다음 반복 횟수로 이동한다.
  - n이 encoding의 index번째 값보다 작거나 같은 경우 해당 위치의 숫자를 소모하고 다음 값을 반환해야 하므로, encoding의 index번째 값에 n을 뺀 후 encoding의 $index + 1$번째 값을 반환한다.
- 반복이 완료되면 반환할 값이 없으므로, -1을 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RLEIterator.java){:target="_blank"}에서 확인 가능합니다.