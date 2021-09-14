---
title: "Python Selenium Chromedriver Timeout"
excerpt: "Python Selenium Chromedriver - session not created
from timeout에 대한 설명"
last_modified_at: 2021-09-14T12:00:00
header:
  image: /assets/images/python/selenium-chromedriver-timeout.png
categories:
  - Python
tags:
  - Programming
  - Python
  - Selenium

toc: true
toc_ads: true
toc_sticky: true
---
# 오류 발생
```python
Python 3.8.12 (default, Sep  3 2021, 02:24:44)
[GCC 10.2.1 20210110] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> from selenium import webdriver
>>> options = webdriver.ChromeOptions()
>>> options.add_argument('--headless')
>>> options.add_argument('--no-sandbox')
>>> options.add_argument('--disable-dev-shm-usage')
>>> driver = webdriver.Chrome(executable_path='/app/chromedriver', chrome_options=options)
<stdin>:1: DeprecationWarning: use options instead of chrome_options
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "/usr/local/lib/python3.8/site-packages/selenium/webdriver/chrome/webdriver.py", line 76, in __init__
    RemoteWebDriver.__init__(
  File "/usr/local/lib/python3.8/site-packages/selenium/webdriver/remote/webdriver.py", line 157, in __init__
    self.start_session(capabilities, browser_profile)
  File "/usr/local/lib/python3.8/site-packages/selenium/webdriver/remote/webdriver.py", line 252, in start_session
    response = self.execute(Command.NEW_SESSION, parameters)
  File "/usr/local/lib/python3.8/site-packages/selenium/webdriver/remote/webdriver.py", line 321, in execute
    self.error_handler.check_response(response)
  File "/usr/local/lib/python3.8/site-packages/selenium/webdriver/remote/errorhandler.py", line 242, in check_response
    raise exception_class(message, screen, stacktrace)
selenium.common.exceptions.SessionNotCreatedException: Message: session not created
from timeout: Timed out receiving message from renderer: 600.000
  (Session info: headless chrome=93.0.4577.63)
```

# 오류 확인
- selenium 모듈로 chromedriver를 이용하여 session을 생성하려고 execute하였으나, reponse를 받지 못하고 timeout으로 SesionNotCreatedException이 발생 한 것으로 확인 되었음.
- chromedriver를 통해 정상적인 session을 생성하지 못했다는(응답이 지연되었다는) 것은 chromedriver을 사용할 경우 문제가 발생하는 이유가 존재하는 것으로 판단 됨.

# 오류 조사
## [Selenium Timed out receiving message from renderer](https://stackoverflow.com/questions/48450594/selenium-timed-out-receiving-message-from-renderer){:target="_blank"}
- Docker container 내부 Testing 결과 1%의 비율로 해당 오류가 발생하는 것으로 판단되었다는 내용.
- [Brandon Schabell의 답변 내용](https://stackoverflow.com/a/48453280){:target="_blank"}과 해당 댓글에 존재하는 [Chromium Bugs - Issue 794017: Linux Chrome startup is flaky on ChromeDriver waterfall without --disable-gpu](https://bugs.chromium.org/p/chromium/issues/detail?id=794017){:target="_blank"} 내용을 참고해보자.
- 위 내용을 읽어보면 VM에서 비정상적으로 GPU를 사용하려는 시도가 있어 Chromedirver를 사용할 경우 '--disable-gpu' 옵션을 사용하면 안정적으로 동작이 가능한 것으로 판단이 된다.

## [How to solve that makes my screen all black](https://www.turnoffthelights.com/support/browser-extension/makes-my-screen-all-black/){:target="_blank"}
- 해당 게시자의 말에 따르면 GPU를 사용하였을 경우, 블랙 스크린(응답 없음)이 발생하여 Disabled 처리하였다는 내용이다.
- 위의 내용에 따르면 특정 환경에서 Windows 또한 GPU를 사용하는 설정이 Chrome에 비정상적인 영향을 발생시킨다는 것을 확인 할 수 있다.

# 결론
1. Chrome의 GPU 사용 기능에는 버그가 존재한다.
- Chrome의 GPU를 사용하는 설정은 물론 애플리케이션의 성능 향상을 위한 옵션으로 개발 된 것으로 판단된다.
- 하지만 GPU를 사용하는 경우에도 해당 설정이 애플리케이션 실행에 치명적인 오류가 발생할 수 있으며, 해당 오류에 대한 처리가 미흡하거나 정확히 파악하지 못한 버그가 존재한다고 볼 수 있다.

2. Chrome을 안정적으로 사용하기 위해서는 GPU 사용 설정을 꺼야한다.
- 모든 OS 환경에서 Chrome을 안정적으로 사용하기 위해서 아직까지는 GPU 사용 설정을 끄는 것이 이로울 듯 하다.
  - 'Windows에서는 설정 > 고급 > 시스템 > 가능한 경우 하드웨어 가속 사용'을 Off로 설정한다.
  - Linux에서는 Chromedriver option에 존재하는 '--disable-gpu'을 실행 Command에 넣어 사용한다.