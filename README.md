# Web-Serv
My First Little Web Server✨

> PDF
>  https://cdn.intra.42.fr/pdf/pdf/103035/en.subject.pdf

## Summary :

URL 이 왜 HTTP 로 시작하는지 마침내 이해할 수 있는 때가 왔다!
이 프로젝트는 나만의 HTTP 서버를 작성하고 실제 브라우저에서 테스트할 수 있다.
HTTP 는 인터넷에서 가장 많이 사용 되는 프로토콜(규약) 중 하나이다. 웹사이트를 개발하지 않더라도 HTTP 의 작동방식을 이해하는 것은 유용할 것이다.

## Introduction
- Hypertext Transfer Protocol (HTTP) 은 분산형, 협력형 하이퍼 미디어 정보 시스스템을 위한 응용프로토콜이다.
- HTTP 는 웹의 기초 데이터 통신을 위한 기반으로, 하이퍼텍스트 문서에는 사용자가 웹 브라우저에서 마우스 클릭이나 화면 탭을 통해 다른 리소스에 쉽게 엑세스할 수 있는 하이퍼핑크가 포함된다.
- HTTP는 하이퍼텍스트 및 월드 와이드 웹 (Word Wide Web) 을 용이하게 하기 위해 개발되었다.
- 웹 서버의 주요 기능은 웹 페이지를 저장, 처리 및 클라이언트에게 전달하는 것이다. 클라이언트와 서버간의 통신은 HTTP 를 사용하여 이루어진다.
- 전달되는 페이지는 주로 HTML 문서이며, 텍스트 콘텐츠 외에도 이미지, 스타일 시트 및 스크립트가 포함될 수 있다.  -> (HTML, CSS, JPG, java script가 이것인가..!)
- 고트래픽 웹사이트에는 여러 웹 서버를 사용할 수 있다.
- 웹 브라우저 또는 웹 크롤러와 같은 사용자 에이전트가 HTTP 를 사용하여 특정 리소스를 요청함으로써 통신이 시작되고, 서버는 해당 리소스의 내용 또는 실패 시 오류 메세지로 응답한다. 리소스는 일반적으로 서버의 보조 저장소에 있는 실제 파일이지만 이것이 항상 그렇지는 않으며 웹 서버의 구현 방식에 따라 다르다.
- 주요 기능은 콘텐츠를 제공하는 것이지만, HTTP의 완전한 구현에는 클라이언트로부터 콘텐츠를 수신하는 방법도 포함된다. 이 기능은 웹 폼 제출을 포함하여 웹 서버로 콘텐츠를 전송하는 데 사용된다.

## General rules
- 프로그램은 어떤 상황에서도 (메모리 릭이 발생하는 경우에도) 크래시(충돌)하거나 예기지 않게 종료해서는 안된다.
- Makefile 제출 해야한다. 리링크는 금지된다. $(NAME), all, clean, fclean, re규칙
- c++ -Wall -Wextra -Werror
- -std=c++98 플래그 추가시 컴파일 가능해야한다.
- 가능한 C++의 기능을 사용하도록 노력애햐한다.
- 외부 라이브러리 및 Boost 라이브러리 사용이 금지된다.

## Mandatory part

| **program name** | webserv |
|--------------|---------|
|** Makefile** |Name, all, clean, fclean, re|
|** Arguments **| [A configuration file] | 
|** External functs| Everything in C++ 98. execve, dup, dup2, pipe, strerror, gai_strerror, errno, dup, dup2, fork, socketpair, htons, htonl, ntohs, ntohl, select, poll, epoll (epoll_create, epoll_ctl, epoll_wait), kqueue (kqueue, kevent), socket, accept, listen, send, recv, chdir bind, connect, getaddrinfo, freeaddrinfo, setsockopt, getsockname, getprotobyname, fcntl, close, read, write, waitpid, kill, signal, access, stat, opendir, readdir and closedir |
|Libft authorized| n/a |
|Description| A HTTP server in c++98|
- C++ 98로 HTTP 서버를 작성해야 한다.
- 실행파일은 다음과 같이 실행된다.
```c++
./webserv [config file]
``` 
<code>epoll()이 주어지고 평가 척도에 언급되었더라도 select(), kqueue(), 또는 epoll()과 같은 동등한 것을 사용할 수 있습니다.</code>

==프로젝트를 시작하기 전에 RFC를 읽고 telnet 및 NGINX를 사용하여 몇 가지 테스트를 수행해라.==
==모든 RFC를 구현할 필요는 없지만 읽어보면 필요한 기능을 개발하는 데 도움이 된다.==

1. 요구사항
    - 프로그램은 구성 파일을 인수로 받거나 기본 경로를 사용해야 한다.
    - 다른 웹 서버를 실행(execve)해서는 안된다.
    - 서버는 절대로 차단되지 않아야 하며 클라이언트가 필요한 경우 올바르게 바운스될 수 있어야 한다.
    - (listen을 포함한) 클라이언트와 서버간의 모든 I/O 작업(수신 포함)에 대해 블로킹되어서는 안되며 (비차단 상태여야 하며) 1개의 poll() (또는 동등한 것)을 사용해야한다.
    - poll() 은 읽기와 쓰기를 동시에 확인해야 한다.
    - 반드시 poll()을 거치지 않고 읽기 또는 쓰기 작업을 수행해서는 안된다.
    - 읽기 또는 쓰기 작업 후 errno 값을 확인하는 것은 엄격히 금지되어 있다
    - 구성파일을 읽기 전에 poll()을 사용할 필요는 없다.
    - ==Non blocking 파일 디스크립터를 사용해야하기 때문에 poll()없이 read/recv 또는 write/send 함수를 사용할 수 있으며, 서버는 차단되지않는다.==
    - ==하지만 시스템 리소스를 더 많이 소비하게 되므로, poll()을 사용하지 않고 파일 디스크립터에서 시도한다면, 당신은 0점.==
    - 모든 매크로를 사용할 수 있으며 FD_SET, FD_CLR, FD_ISSET, FD_ZERO와 같이 define 할 수 있다. (매크로가 무엇을 어떻게 수행하는지 이해하면 매우 유용할 것!)
    - 서버에 대한 요청이 영원히 중단되지 않아야 한다.
    - 서버는 선택한 웹 브라우저와 호환되어야 한다.
    - NGINX는 HTTP 1.1을 준수하며 헤더와 응답 동작을 비교하는 데 사용될 수 있다.
    - HTTP 응답 상태 코드가 정확해야 한다.
    - 기본 오류 페이지가 제공되지 않는 경우 서버에 기본 오류 페이지가 있어야 한다.
    - fork를 CGI 가 아닌 다른 것 (ex: PHP, Python 등)에 사용할 수 없다.
    - 완전히 정적인 static 웹 사이트를 제공할 수 있어야 한다.
    - 클라이언트가 파일을 업로드 할 수 있어야 한다.
    - 최소한 GET, POST, DELETE 메서드가 있어야 한다.
    - 빡센 테스트를 해라. 서버는 항상 사용 가능한 상태를 유지해야 한다.
    - 서버는 여러 포트를 수신할 수 있어야 한다. (configuration file 참조)

2. MacOS 전용
    - MacOS는 다른 유닉스 OS와 같은 방식으로 write()를 구현하지 않으므로 fcntl()을 사용할 수 있다.
    - 다른 유닉스OS와 유사한 동작을 얻으려면 비동기 모드에서 파일 디스크립터를 사용해야 한다.
    - 그러다 다음과 같은 경우에만 fcntl()을 사용할 수 있다.
    - `fcntl(fd, F_SETFL, O_NONBLOCK, FD_CLOEXEC);`
    - 다른 플래그는 금지된다.

3. 구성파일(Configuration file)
   ==NGINX의 `server` 부분에서 영감을 얻을 수 있다.
    - 구성 파일에서 다음을 수행할 수 있어야 한다.
        - 각 `server`의 port와 host를 선택한다.
        - `server_names`를 설정할지 여부를 정한다.
        - host : port의 첫 번째 서버가 이 host:port의 기본값이 된다. (다른 서버에 속하지 않은 모든 요청에 응답한다는 의미)
        - 기본 오류 페이지를 설정한다.
        - 클라이언트의 body(본문) 사이즈를 제한한다.
        - 다음 규칙/구성 중 하나 또는 여러개를 사용하여 경로(라우터)를 설정한다. (경로에 정규식을 사용하지 않는다.)
            - 경로에 허용되는 HTTP 메소드 목록을 정의한다.
            - HTTP 리다이렉션을 정의한다.
            - 파일을 검색할 디렉토리 또는 파일을 정의한다. (ex: url /kapouet이 /tmp/www에 루팅된 경우, url /kapouet/pouic/toto/pouet은 /tmp/www/pouic/toto/pouet이다.)
            - 디렉토리 목록을 켜거나 끈다.
            - 요청이 디렉토리인 경우 응답할 기본 파일을 설정한다.
            - 특정 파일 확장자(ex: php)를 기준으로 CGI를 실행한다.
            - POST, GET 메서드와 함께 동작하도록 설정한다.
            - 업로드 된 파일을 허용하고 저장할 위치를 설정할 수 있는 경로를 만든다.
                - CGI가 뭔지 궁금하신가요? -> https://en.wikipedia.org/wiki/Common_Gateway_Interface
                - CGI를 직접 호출하지 않으므로 전체 경로를 PATH_INFO로 사용해라.
                - chunked request의 경우 서버가 chunk를 unchunk 해야하며, CGI는 본문의 끝을 EOF로 예상한다는 점을 기억해라.
                - CGI의 출력도 마찬가지이다. CGI에서 content_length가 반환되지 않으면, EOF는 반환된 데이터의 끝을 표시한다.
                - 프로그램은 요청된 파일을 첫 번째 인수로 사용하여 CGI를 호출해야 한다.
                - CGI는 상대 경로 파일 액세스(허용)을 위해 올바른 디렉토리에서 실행되어야 한다.
                - 서버는 하나의 CGI(php-CGI, Python 등)로 작동해야 한다.

    - 평가 과정에서 모든 기능이 작동하는지 테스트하고 시연할 수 있도록 몇 가지 구성 파일과 default basic file을 제공해야 한다.
    - ==한 동작에 대한 질문이 있는 경우 프로그램 동작과 NGINX의 동작을 비교해야 한다.==
    - ==예를 들어 server_name이 어떻게 작동하는지 확인해라.
    - ==작은 테스터를 공유했다. 브라우저와 테스트에서 모든것이 정상적으로 작동한다면 반드시 통과해야하는 것은 아니지만 버그를찾는 데 도움이 될 수 있다!==
    - **중요한 것은 복원력이다. 서버가 죽어서는 안된다.
    - **한 가지 프로그램으로 테스트 하지 말 것. Python이나 Golang 등 더 편리한 언어로 테스트를 작성해라. 원한다면 C나 C++로도 가능하다.

## Bonus part
- 추가할 수 있는 기능은 다음과 같다.
    - 쿠키 및 세션 관리 지원 (간단한 예제 준비)
    - 여러 CGI를 처리한다.


-------

## **평가 준비**

- *Todo*
    - 1. Check the code and ask questions
        - [x] Launch the installation of *siege* with homebrew
        - [x] HTTP server에 대한 기본적인 설명
        - [x] I/O 멀티플렉싱을 사용하기 위해 어떤 함수를 사용했는지 -> 우리는 Kqueue 사용
        - [x] epoll() (or equivalent)의 작동방식에 대한 설명
        - [x] kqueue()를 하나만 사용하는지, 서버가 accept하고 클라이언트가 read/write 하는 것을 어떻게 관리하는지 설명
        - [x] kqueue()는 main loop 에 있어야 하며, fd가 read/write를 **동시에** 확인해야한다. 그렇지 않으면 0점, 평가종료
        - [x] There should be only one read or one write per client per kqueue().
          kqueue()에서 클라이언트의 읽기/쓰기에 대한 코드 보여주기.
        - [ ] 소켓에서 read/recv/write/send를 검색하고 오류가 반환되면 클라이언트가 지워지는지 확인
        - [ ] 모든 read/recv/write/send를 검색하고 반한된 값이 올바르게 확인되었는지 체크. (-1 또는 0 값만 확인하는것만으로는 충분하지 않으며 둘다 확인해야한다.)
          > 0 ||  == 0 || < 0 모두 체크 할 것
        - [x] read/recv/write/send 후 errno를 체크하면 성적은 0점, 평가 종료!
        - [x] kqueue()를 거치지 않고 fd를 읽거나 쓰는 것은 엄격하게 금지되어있다.
        - [x] 컴파일 잘되어야한다. 리링크 되면 안된다.
        - [ ] 위의 내용이 하나라도 올바르지 않으면 평가 중단.
    - 2. Configuration
        - [ ] HTTP status code 를 검색합니다. 평가 중 상태코드가 잘못 된 경우 관련 점수를 주지말 것.
        - [x] 포트가 다른 여러 서버를 설정한다.
        - [ ] 호스트 이름이 다른 여러 서버를 설정한다. (use something like: curl --resolve example.com:80:127.0.0.1 http://example.com/ (http://example.com/)). ---------->?무슨 소리인지 잘 모르겠음.. 클러스터 맥에서는 안된다고함.
        - [x] defult error page를 설정한다. (404 에러 변경 시도)
        - [ ] 클라이언트 본문 제한 (use: curl -X POST -H "Content-Type: plain/text" --data "BODY IS HERE write something shorter or longer than body limit")
        - [ ] 서버에서 다른 디렉토리로 향하는 경로 설정
        - [ ] 디렉토리 요청시 검색할 기본  파일 설정
        - [ ] Setup a list of methods accepted for a certain route (e.g., try to delete something with and without permission).
    - 3. Basic checks
        - telnet, curl, prepared files을 사용하여 다음 기능이 작동하는지 확인 :
        - [ ] GET, POST DELETE 요청이 작동해야 한다.
        - [ ] UNKNOWN 요청으로 인한 crash 가 발생하면 안된다.
        - [ ] 모든 테스트에서 적절한 상태코드를 받아야 한다.
        - [ ] 서버에 파일을 업로드하고 다시 받기.
    - 4. CheckCGI
        - [ ] 서버가 CGI를 사용하여 정상적으로 작동하는지
        - [ ] 상대 경로 파일 액세스를 위해 올바른 디렉토리에서 실행되어야 한다.
		       The CGI should be run in the correct directory for relative path file access.
        - [ ] GET POST 메서드를 사용하여 CGI를 테스트 해야한다.
          With the help of the students you should check that everything is working properly. You have to test the CGI with the "GET" and "POST" methods.
        - [ ] 오류가 포함된 파일로 테스트하여 error handling이 제대로 작동하는지 확인해야 한다. 무한루프 또는 에러가 포함된 스크립트를 사용할 수 있으며, 허용 가능한 한도 내에서 재량에 따라 원하는 테스트를 자유롭게 수행할 수 있다. 평가 대상 그룹이 이를 도와줄 것.
        - [ ] 서버가 다운되지 않아야 하며 문제 발생 시 오류가 표시되어야 한다.
    - 5. Check with a browser
        - [ ] reference browser를 사용한다. 네트워크 부분을 열고 이를 사용하여 서버에 연결을 시도한다.
        - [ ] 요청 헤더와 응답헤더를 확인한다.
        - [ ] 완전히 정적인 웹사이트를 제공하는데 아무런 문제가 없어야 한다.
        - [ ]  Try a wrong URL on the server.
        - [ ] Try to list a directory.
        - [ ] Try a redirected URL.
        - [ ] Try anything you want to.
    - 6. Port issues
        - [ ] configuration file에서 여러 포트 설정하고 서로 다른 웹사이트 사용해보기.
          브라우저를 사용하여 구성이 예상대로 작동하고 올바른 웹사이트를 표시하는지 확인
        - [ ] 구성파일에서 동일한 포트를 여러 번 설정해보기. 작동하지 않아야 한다.
          -> bind error 발생해야함.
        - [ ] 구성파일은 다르지만 같은 포트를 사용하여 여러서버를 동시에 시작해라.
          -> config file에 동일한 포트 2개이상 설정시 bind error 발생해야함.
            - [ ] 작동하나요? 작동한다면, 구성 중 하나가 작동하지 않은경우에 서버가 작동해야만 하는 이유를 물어봐라.
              Launch multiple servers at the same time with different configurations but with common ports. Does it work? If it does, ask why the server should work  if one of the configurations isn’t functional. Keep going.
    - 7. Siege & stress test
        -  Use Siege to run some stress tests.
        - [ ] Availability should be above 99.5% for a simple GET on an empty page with a siege -b on that page.
        - [ ] Verify there is no memory leak (Monitor the process memory usage. It should not go up indefinitely).
        - [ ] Check if there is no hanging connection.
          `lsof -Pni4 | grep LISTEN`
        - [ ] You should be able to use siege indefinitely without having to restart the server (take a look at siege -b).
        - [ ] - `while ; do leaks [ps] ; sleep 3 ; clear ; done`
    - *BONUS
        - Cookies and session
        - [ ]  There is a working session and cookies system on the webserver
        - 테스트 하는 방법은 간단하다. 쿠키를 확인하기 위해서는 클라이언트로 브라우저를 사용해야한다.
            1. webserv config file로 default.conf 를 사용한다.
            2. localhost:442/session 으로 요청을 보낸다.
            3. 사용자 도구 -> 애플리케이션 -> 쿠키에서 세션id가 생성되었는지 확인한다.
            4. localhost:442/session/delete 에 요청을 한번 더 날리고 쿠키에 세션id를 지울 수 있다.
        - CGI
            - [ ]  There is more than one CGI system
 