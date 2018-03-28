# Unix와 Linux
[참고자료](https://www.techworm.net/2016/11/difference-linux-unix-operating-systems.html)  
[참고자료](https://www.quora.com/Is-Mac-OS-X-essentially-built-on-top-of-Linux)

## Unix os
* 1971년, Bell Labs에서 Ken Thompson, Dennis Ritchie과 같은 사람들에 의해 만들어졌다
* 연구소내에서 자체적으로 사용할 목적이었으나 몇 년 후 다른 기술회사들에게 라이센싱됨
* 주로 커맨드 라인으로 작동했지만 최근에 GUI(graphical user interface)가 개발됨
* **무료가 아님.** 그래서 오픈 소스를 이용할 수 없음
* 리눅스보다 유연하지 않고 하드웨어 호환성이 떨어진다. 따라서 unix만을 위해 만들어진 cpu가 필요
* 이런 하드웨어, 소프트웨어적인 특성 떄문에 unix를 이용하려면 비용이 많이 든다.
* 주로, 대형의 빅데이터 서버나 메인프레임워크, 하이엔드 컴퓨터에 사용된다.
* solaris가 대표적

## Linux os
* 1991년 Linus Torvalds가 개발
* unix에 기반을 둔 오픈소스 os(unix-like os라고도 함)
* 개발 당시 GUI를 가지고 있어서 사용이 쉬웠음(커맨드라인도 물론 이용 가능)
* **무료**에다가 유연성이 뛰어나 하드웨어 호환성이 좋음
* 가정용으로 초점에 맞춰 개발되었으나 높은 인기와 안정성 때문에 회사나 하이엔드 시스템에 사용됨
* BASH (Bourne Again SHell)가 linux os의 디폴트 쉘이다
* Ubuntu가 대표적

**둘다 같은 linux 커맨드 라인을 제공한다**

참고로 mac os도 unix-like os이다(BSD)
```

     +----------- Unix - - - - - -+
     | (modify)           (clone) | 
    BSD                          GNU
     |      (replace kernel)      |
Darwin/OS X                     Linux
```