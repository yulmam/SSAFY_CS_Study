# SSAFY_CS_Study

## CS 관련 지식

### 네트워크

<details>
  <summary>웹 통신의 큰 흐름: https://www&#46;google&#46;com/ 을 접속할 때 일어나는 일</summary>
  </br>
  <p>면접 단골 문제입니다. 면접관 입장에서는 한 질문으로 많은 답변을 들을 수 있기 때문에 대부분의 면접자리에서 나왔던 문제입니다. OSI 7계층과도 연관지어 설명하라는 질문을 받은적도 있습니다.</p>
  <p>브라우저가 URL에 적힌 값을 파싱해서 HTTP Request Message를 만들고, OS에 전송 요청을 합니다. 이 때, Domain으로 요청을 보낼 수 없기 때문에 DNS Lookup을 수행합니다.</p>
  <p>DNS 룩업 과정은 크롬의 경우 브라우저 → hosts 파일 → DNS Cache의 순서로 도메인에 매칭되는 ip를 찾습니다. 일반적으로 설명하는 DNS Lookup은 루트 도메인서버에서부터 서브도메인 서버순으로 찾게됩니다.</p>
  <p>이 요청은 프로토콜 스택이라는 OS에 내장된 네트워크 제어용 소프트웨어에 의해 패킷에 담기고 패킷에 제어정보를 덧붙여 LAN 어댑터에 전송하고, LAN 어댑터는 이를 전기신호로 변환시켜 송출합니다.</p>
  <p>패킷은 스위칭 허브 등을 경유하여 인터넷 접속용 라우터에서 ISP로 전달되고 인터넷으로 이동합니다.</br>
액세스 회선에 의해 통신사용 라우터로 운반되고 인터넷의 핵심부로 전달됩니다. 고속 라우터들 사이로 목적지까지 패킷이 흘러들어가게 됩니다.</p>
  <p>핵심부를 통과한 패킷은 목적지의 LAN에 도착하고, 방화벽이 패킷을 검사한 후 캐시 서버로 보내어 웹 서버에 갈 필요가 있는지 검사합니다.</p>
  <p>웹 서버에 도착한 패킷은 프로토콜 스택이 패킷을 추출하여 메시지를 복원하고 웹 서버 애플리케이션에 넘깁니다. 애플리케이션은 요청에 대한 응답 데이터를 작성하여 클라이언트로 회송하고, 이는 전달된 방식 그대로 전송됩니다.</p>
</details>

<details>
  <summary>TCP와 UDP의 차이점에 대해서 설명해보세요.</summary>
  </br>
  <p>TCP는 연결 지향형 프로토콜이고 UDP는 데이터를 데이터그램단위로 전송하는 프로토콜입니다.</p>
  <p>TCP는 가상 회선을 만들어 신뢰성을 보장하도록(흐름 제어, 혼잡 제어, 오류 제어) 하는 프로토콜로 따로 신뢰성을 보장하기 위한 절차가 없는 UDP에 비해 속도가 느린편입니다.</p>
  <p>TCP는 그래서 파일전송과 같은 신뢰성이 중요한 서비스에 사용되고, UDP는 스트리밍, RTP와 같이 연속성이 더 중요한 서비스에 사용됩니다.</p>
  <p>+) 하지만 UDP도 신뢰성을 UDP자체에서 보장하지 않는 것 뿐이지, 개발자가 직접 신뢰성을 보장하도록 할 수 있습니다. 그래서 HTTP/3은 QUIC이라는 프로토콜을 기반으로 하는데, QUIC은 UDP를 기반으로 합니다. 즉, UDP 자체는 신뢰성을 보장하지 않지만, 추가적인 정의를 통해 신뢰성을 보장받을 수 있습니다.</p>
</details>

<details>
  <summary>TCP 3, 4 way handshake에 대해서 설명해보세요.</summary>
  </br>
  <p>TCP가 가상회선을 만들고 제거하는 과정에 대해서 묻는 질문입니다. TCP를 공부하셨다면 이 정도는 알겠지 하고 묻는 문제고, 실제 면접자리에서는 보통 네트워크에 대해서 설명할 때, 직접 설명하는 편입니다.</p>
  <p>TCP 3way handshake는 가상회선을 수립하는 단계입니다. 클라이언트는 서버에 요청을 전송할 수 있는지, 서버는 클라이언트에게 응답을 전송할 수 있는지 확인하는 과정입니다. SYN, ACK 패킷을 주고받으며, 임의의 난수로 SYN 플래그를 전송하고, ACK 플래그에는 1을 더한값을 전송합니다. 정확한 순서는 SYN(n) -> ACK(n + 1), SYN(m) -> ACK(m + 1) 순으로 일어납니다.</p>
  <p>왜 임의의 난수를 지정하느냐는 꼬리질문이 나올 수 있습니다. 기존 요청과 구분하기 위해서 정도로 알고있고, 그 이상은 생각해본적이 없네요.</p>
  </br>
  <p>TCP 4way handshake는 TCP연결을 해제하는 단계로, 클라이언트는 서버에게 연결해제를 통지하고 서버가 이를 확인하고 클라이언트에게 이를 받았음을 전송해주고 최종적으로 연결이 해제됩니다. 단, 서버에서 소켓이 닫혔다고 통지해도 클라이언트 측에서는 일정시간 대기하는데, 혹시나 패킷이 나중에 도착할 수 있기 때문입니다.</p>
</details>

<details>
  <summary>HTTP와 HTTPS의 차이점에 대해서 설명해보세요.</summary>
  </br>
  <p>HTTP는 따로 암호화 과정을 거치지 않기 때문에 중간에 패킷을 가로챌 수 있고, 수정할 수 있습니다. 따라서 보안이 취약해짐을 알 수 있습니다. 이를 보완하기 위해 나온 것이 HTTPS입니다. 중간에 암호화 계층을 거쳐서 패킷을 암호화합니다.</p>
</details>

<details>
  <summary>HTTPS에 대해서 설명하고 SSL Handshake에 대해서 설명해보세요.</summary>
  </br>
  <p>HTTPS는 HTTP에 보안 계층을 추가한 것입니다. HTTPS는 제3자 인증, 공개키 암호화, 비밀키 암호화를 사용합니다.</p>
  <p>제3자 인증은 믿을 수 있는 인증기관에 등록된 인증서만 신뢰하는 것이고, 공개키 암호화는 비밀키를 공유하기 위해 사용합니다. 비밀키 암호화는 통신하는 데이터를 암호화하는데 사용합니다.</p>
  <p>클라이언트는 TCP 3way handshake를 수행한 이후 Client Hello를 전송합니다. 서버는 인증서를 보냅니다.(다른 정보들도 전송하나 검색을 통해 알 수 있는 부분입니다. 대개 그 정도까지는 요구하지 않습니다.)</p>
  <p>클라이언트는 받은 인증서를 신뢰하기 위해서 등록된 인증기관인지 확인합니다. 이 인증서는 인증기관의 개인키로 암호화되어있고, 공개키로 검증할 수 있습니다.(브라우저에 내장되어있음) 클라이언트는 사이트의 정보와, 서버의 공개키를 얻을 수 있습니다.</p>
  <p>서버의 공개키로 통신에 사용할 비밀키를 암호화해서 서버에 보냅니다. 서버는 이를 개인키로 확인하고 이후 통신은 공유된 비밀키로 암호화되어 통신합니다.</p>
  <p>제3자 인증: 인증서, 인증기관/공개키 암호화: 인증서, 비밀키 공유/비밀키 암호화: 통신과정</p>
  <p>왜 공개키 암호화와 비밀키 암호화를 복합적으로 사용했는지도 질문을 받았습니다.</p>
</details>

<details>
  <summary>GET과 POST의 차이점에 대해서 설명해보세요.</summary>
  </br>
  <p>대개의 경우 아래의 HTTP 메서드 질문을 더 많이합니다. 하지만 둘의 차이만을 물을 수도 있습니다.</p>
  <p>GET요청은 서버에 존재하는 정보를 요청합니다. 이 때 반환되는 정보는 정보 자체가 아니라 정보의 표현입니다.(뒤의 내용은 REST와 연관이 있고, 굳이 답변하지 않으셔도 됩니다.) 일반적으로 Request Body는 입력하지 않는 것이 일반적이며, 레거시 시스템의 경우 요청을 받아들이지 않을 수 있습니다. 캐싱을 수행하기 때문에 캐싱되지 않는 요청은 GET 요청이 맞지 않을 수 있습니다.</p>
  <p>POST요청은 서버에 정보를 생성하는 것을 요청합니다. 예전 HTTP 통신은 POST 요청으로 데이터 삭제, 수정도 form요청으로 같이 수행했습니다. POST 요청은 서버의 상태를 변경시키기 때문에 멱등성이 유지되지 않습니다. 보통 Request Body에 요청하는 데이터를 담아 전송합니다.</p>
</details>

<details>
  <summary>HTTP 메서드와 이것이 하는 역할에 대해서 설명해보세요.</summary>
  </br>
  <p>보통 REST API를 설계했다면 이해할 수 있을정도로 설명하면 되는 것 같습니다.</p>
  <p>OPTIONS, HEAD, TRACE의 존재에 대해서는 알아만 둡시다. 특히 TRACE는 몰라도 되는 것 같습니다. OPTIONS는 해당 uri에 대해 서버가 허용하는 메서드를 확인할 때 사용합니다. HEAD는 GET과 비슷하나 header만 가져옵니다.</p>
  <ul>
    <li>GET 요청은 서버에 존재하는 데이터를 요청하는 것입니다. CRUD로 따지면 R입니다.</li>
    <li>POST 요청은 서버에 데이터를 생성하는 것을 요청합니다. CRUD로 따지면 C입니다.</li>
    <li>PUT 요청은 서버에 존재하는 데이터를 수정하거나 존재하지 않으면 생성합니다. CRUD로 따지면 C,U입니다.</li>
    <li>DELETE 요청은 서버에 데이터를 제거할 것을 요청합니다. 존재하지 않아도 동일하게 동작합니다. CRUD로 따지면 D입니다.</li>
    <li>PATCH 요청은 서버에 존재하는 데이터를 일부 수정합니다. CRUD로 따지면 U입니다.</li>
  </ul>
  <p>더 나아가서 불필요한 메서드는 허용하지 않고 필요한 메서드만 허용하는 Whitelist 방식으로 관리합시다. 자세한 내용은 HTTP Method 취약점에 대해 검색합시다.</p>
</details>

<details>
  <summary>RESTful이란 무엇이며, 이것에 대해서 아는대로 설명해보세요.(보충필요)</summary>
  </br>
  <p>REST는 굉장히 난해한 개념입니다. 하지만 REST가 무엇인지 대략의 감은 잡아둡시다. REST API를 설계했다면 충분히 물어볼만한 질문입니다.</p>
  <p>HTTP URI를 통해 자원을 표시하고 HTTP Method를 통해 자원에 대한 처리를 표현합니다. 사람이 읽을 수 있는 API라는 것이 특징입니다. HTTP를 사용하기 때문에 HTTP의 특성을 그대로 반영합니다. 또한 별도의 인프라 구축이 필요없습니다.</p>
  <p>단점으로는 명확한 표준이 존재하지 않는다는 점, RESTful을 완전히 만족하는 API를 만들기는 매우 까다롭다는 점(그런 REST API로 괜찮은가 참고)이 있습니다.</p>
  <p>HATEOAS라는 개념이 있는데, 동적인 API를 제공할 수 있게됩니다.(모든 관련된 동작을 URI를 통해 알려줍니다.) 즉, 클라이언트가 API의 변화에 일일이 대응하지 않아도 된다는 장점을 가져옵니다.</p>
</details>

<details>
  <summary>CORS란 무엇이며 이것에 대해서 설명해보세요.</summary>
  </br>
  <p>CORS는 웹개발을 하다가 흔히 만날 수 있는 이슈입니다. 대개는 프론트엔드 개발시에 로컬에서 API 서버에 요청을 보낼 때 흔하게 발생합니다.</p>
  <p>서로 다른 도메인간에 자원을 공유하는 것을 뜻합니다. 대부분의 브라우저에서는 이를 기본적으로 차단하며, 서버측에서 헤더를 통해서 사용가능한 자원을 알려줍니다.</p>
  <p>preflight request는 실제 요청을 보내도 안전한지 판단하기 위해 사전에 보내는 요청입니다. OPTIONS 메서드로 요청하며 CORS를 허용하는지 확인합니다. CORS가 허용된 웹서버라면 사용 가능한 리소스를 헤더에 담아 응답합니다.</p>
</details>

<details>
  <summary>OSI7계층과 그 존재 이유, TCP/IP 4계층에 대해 설명해보세요.</summary>
  </br>
  <p>OSI7계층은 네트워크 통신을 구성하는 요소들 7개의 계층으로 표준화 한 것입니다. 이렇게 표준화하는 것의 장점은 통신이 일어나는 과정을 단계별로 파악할 수 있어, 문제가 발생하면 해당 문제를 해결하기 용이해집니다.</p>
  <p>실제로 우리가 대부분 사용하는 네트워크는 TCP/IP 4계층입니다. 통신에 실제로 사용되는 계층이고 1,2 계층이 1계층, 5, 6, 7계층이 4계층으로 운영됩니다.</p>
</details>

<details>
  <summary>웹 서버 소프트웨어(Apache, Nginx)는 OSI 7계층 중 어디서 작동하는지 설명해보세요.</summary>
  </br>
  <p>Apache와 NGINX는 HTTP 웹 서버로, 이들이 동작하는 HTTP 프로토콜은 OSI 7 Layer 중 7계층인 애플리케이션 Layer 에 해당하는 프로토콜입니다. HTTP 프로토콜은 TCP/IP 프로토콜을 통해 동작합니다. TCP/IP 프로토콜은 OSI 7 Layer 중 4계층인 Transport Layer에서 동작합니다.  따라서 웹 서버 소프트웨어는 4계층의 TCP/IP 프로토콜과 7계층의 HTTP 프로토콜을 활용하여 동작합니다.</p>
</details>

<details>
  <summary>웹 서버 소프트웨어(Apache, Nginx)의 서버 간 라우팅 기능은 OSI 7계층 중 어디서 작동하는지 설명해보세요.</summary>
  </br>
  <p> 두 가지가 있습니다. Layer 4 (Transport Layer), 그리고 Layer 7 (Application Layer) 입니다. L4 에서는 TCP/UDP 포트 정보를 토대로 라우팅 기능이 제공됩니다. L7에서는 TCP/UDP 뿐만 아니라 HTTP의 URI 등을 토대로 라우팅 기능이 제공 됩니다. 
  L4 에서 라우팅 기능을 사용 한 예시를 들자면, Nginx 의 경우 여러 포트들을 하나의 upstream 블록으로 묶어서 로드 밸런싱, 즉 특정 경로로 전달되는 요청을 각 포트 별로 분산해서 전달하도록 설정 해 줄 수 있습니다.
  L7 에서 라우팅 기능을 사용 한 예시를 들자면, Apache, Nginx 각각에서 서브 도메인에 대해 라우팅 설정을 해 둘 수 있습니다. 브라우저에서 /test 와 같은 서브 도메인으로 HTTP 프로토콜을 통한 요청을 보낸다면, 웹서버 내 Config 파일에 설정 된 경로 정보를 토대로 요청에 대한 라우팅을 제공하여 스태틱 파일을 전달하거나 API 서버에 대해 리버스 프록시 역할을 해 줄 수 있습니다.</p>
</details>

### 운영체제

운영체제는 제가 공부가 부족해서 틀리거나 다른 내용이 있을 수 있습니다.  
검색을 통해서 학습하시고, 간단한 자신만의 답을 만들어보세요.  
보통 중요하다곤 하나 지엽적인 지식은 잘 안물어보기도 합니다.(비전공자의 경우 더더욱 물어보지 않을 가능성이 큽니다.)

<details>
  <summary>프로세스와 스레드의 차이를 설명해보세요.</summary>
  </br>
  <p>프로세스는 실행중인 프로그램을 의미합니다. 스레드는 실행 제어만 분리한 것을 의미합니다.</p>
  <p>프로세스는 운영체제로부터 자원을 할당받지만, 스레드는 프로세스로부터 자원을 할당받고, 프로세스의 코드/데이터/힙영역을 공유하기 때문에 좀 더 효율적으로 통신할 수 있습니다. 또한 컨텍스트 스위칭도 캐시 메모리를 비우지 않아도 되는 스레드쪽이 빠릅니다. 그리고, 스레드는 자원 공유로 인해 문제가 발생할 수 있으니 이를 염두에 둔 프로그래밍을 해야합니다.</p>
  <p>한 프로세스 안에 여러개의 스레드가 생성될 수 있습니다.</p>
</details>

<details>
  <summary>컨텍스트 스위칭에 대해 설명해보세요.</summary>
  </br>
  <p>컨텍스트 스위칭은 한 Task가 끝날 때까지 기다리는 것이 아니라 여러 작업을 번갈아가며 실행해서 동시에 처리될 수 있도록 하는 방법입니다.</p>
  <p>인터럽트가 발생하면 현재 프로세스의 상태를 PCB에 저장하고 새로운 프로세스의 상태를 레지스터에 저장하는 방식으로 동작합니다. 이 때, CPU는 아무런 일을 하지 않으므로 잦은 컨텍스트 스위칭은 성능저하를 일으킬 수 있습니다.</p>
  <p>스레드와 프로세스의 동작방식이 약간 상이한데, 스레드는 캐시메모리나 PCB에 저장해야하는 내용이 적고, 비워야 하는 내용도 적기때문에 상대적으로 더 빠른 컨텍스트 스위칭이 일어날 수 있습니다.</p>
</details>

<details>
  <summary>동기와 비동기의 차이(블로킹, 넌블로킹) / 장단점에 대해 설명해보세요.</summary>
  </br>
  <p>동기/비동기는 두 개 이상의 무엇인가가 시간을 맞춘다/안맞춘다로 구분할 수 있습니다.</p>
  <p>동기 방식은 메서드 리턴과 결과를 전달받는 시간이 일치하는 명령 실행 방식입니다. 또, 동기 방식은 한 함수가 끝나는 시간과 바로 다음의 함수가 시작하는 시간이 같습니다.</p>
  <p>비동기 방식은 여러 개의 처리가 함께 실행되는 방식으로, 동기 방식에 비해 단위시간 당 많은 작업을 처리할 수 있습니다. 단, CPU나 메모리를 많이 사용하는 작업을 비동기로 처리하게 되면 과부하가 걸릴 수 있습니다. 프로그램의 복잡도도 증가하게 됩니다.</p>
  <p>블로킹/논블로킹은 동기/비동기와는 다른 관점으로, 내가 직접 제어할 수 없는 대상(IO/멀티스레드)을 상대하는 방법에 대한 분류입니다.</p>
  <p>블로킹 방식은 대상의 작업이 끝날 때 까지 제어권을 대상이 가지고 있는 것을 의미합니다. 반면에 논블로킹은 대상의 작업 완료여부와 상관없이 새로운 작업을 수행합니다.</p>
  <p>동기 논블로킹은 계속해서 polling을 수행하기 때문에 컨텍스트 스위칭이 지속적으로 발생해 지연이 발생합니다.</p>
  <p>https://youtu.be/HKlUvCv9hvA 를 참고합시다.</p>
</details>

<details>
  <summary>멀티스레드 프로그래밍에 대해 설명해보세요.</summary>
  </br>
  <p>멀티스레드 프로그래밍은 하나의 프로세스에서 여러개의 스레드를 만들어 자원의 생성과 관리의 중복을 최소화하는 것을 멀티스레드 프로그래밍이라고 합니다.</p>
  <p>장점
    <ul>
      <li>멀티 프로세스에 비해 메모리 자원소모가 줄어듭니다.</li>
      <li>힙 영역을 통해서 스레드간 통신이 가능해서 프로세스간 통신보다 간단합니다.</li>
      <li>스레드의 컨텍스트 스위칭은 프로세스의 컨텍스트 스위칭보다 빠릅니다.</li>
    </ul>
  </p>
  <p>단점
    <ul>
      <li>힙 영역에 있는 자원을 사용할 때는 동기화를 해야합니다.</li>
      <li>동기화를 위해서 락을 과도하게 사용하면 성능이 저하될 수 있습니다.</li>
      <li>하나의 스레드가 비정상적으로 동작하면 다른 스레드도 종료될 수 있습니다.</li>
    </ul>
  </p>
</details>

<details>
  <summary>Thread-safe 하다는 의미와 설계하는 법을 설명해보세요.</summary>
  </br>
  <p>두 개 이상의 스레드가 race condition에 들어가거나 같은 객체에 동시에 접근해도 연산결과의 정합성이 보장될 수 있게끔 메모리 가시성이 확보된 상태를 의미합니다.</p>
  <ul>
    <li>java.util.concurrent 패키지 하위의 클래스를 사용합니다.</li>
    <li>인스턴스 변수를 두지 않습니다.</li>
    <li>Singleton 패턴을 사용합니다.(이 때, 일반적으로 구현하는 Singleton Pattern은 Thread-safe 하지 않습니다.)[참고](https://github.com/ksundong/TIL/blob/master/DesignPattern/singleton-pattern.md)</li>
    <li>동기화(syncronized) 블럭에서 연산을 수행합니다.</li>
  </ul>
</details>

<details>
  <summary>프로세스 동기화에 대해 설명해보세요.</summary>
  </br>
  <p>알아야 하는 부분이 조금 많습니다. 면접때에는 적절히 짧게 끊어서 대답합시다. 너무 깊게 들어가면 말을 번복할 가능성도 있고, 잘 모른다는 인상을 주기 쉽습니다.</p>
  <p>다중 프로세스 환경에서 자원등에 한 프로세스만이 접근가능하도록 하는 것입니다.</p>
  <p>프로세스 동기화를 하지 않으면 데이터의 일관성이 깨지기 때문에 연산결과가 잘못 반환될 가능성이 존재하기 때문에 주의해야 합니다.</p>
  <p>Race Condition(경쟁 상태): 여러 프로세스나 스레드가 동기화 메커니즘 없이 자원에 접근하려는 상황을 가리킵니다. 공유된 자원에 대한 접근 순서에 따라 실행 결과가 달라질 수 있는 상황을 의미합니다.</p>
  <p>Critical Section(임계 구역): 여러 스레드가 동시에 접근해서는 안되는 공유자원에 접근하는 코드 블럭을 얘기합니다. 한 임계구역에 하나의 스레드 혹은 프로세스만 접근이 가능합니다. 임계 구역에 접근하는 것을 제어하기 위해 세마포어, 뮤텍스와 같은 매커니즘을 사용합니다.</p>
  <p>임계 구역 문제를 해결하기 위한 조건(모두 충족해야함)
    <ul>
      <li>상호 배제(Mutual Exclusion): 한 프로세스가 임계구역에서 동작중이면 다른 프로세스는 접근할 수 없다.</li>
      <li>진행(Progress): 임계구역에서 작업중인 프로세스가 없다면 입계구역으로 진입하려는 프로세스를 적절히 선택해서 진입할 수 있도록 합니다.</li>
      <li>유한 대기(Bounded Waiting): 한 프로세스가 임계영역으로 진입을 요청한 후 다른 프로세스는 진입이 유한한 횟수로 제한되어야 합니다. (기아상태 방지)</li>
    </ul>
  </p>
</details>

<details>
  <summary>교착상태와 기아상태의 해결방법에 대해 설명해보세요.</summary>
  </br>
  <p>교착상태(Deadlock)가 무엇인지 알고 있어야 합니다. 서로 다른 프로세스가 서로 점유하고 있는 자원의 반납을 대기하고 있는 상태를 의미합니다.</p>
  <p>발생조건
    <ul>
      <li>상호 배제: 한 번에 한 프로세스만 해당 자원을 사용할 수 있어야 합니다.</li>
      <li>점유 대기: 할당된 자원을 가진 상태에서 다른 자원을 기다립니다.</li>
      <li>비선점: 다른 프로세스가 자원의 사용을 끝낼 때 까지 자원을 뺏을 수 없습니다.</li>
      <li>순환대기: 각 프로세스가 순환적으로 다음 프로세스가 요구하는 자원을 가지고 있습니다.</li>
    </ul>
  </p>
  <p>해결방법
    <ul>
      <li>예방: 4가지 조건 중 하나라도 만족되지 않도록 합니다.</li>
      <li>회피: 알고리즘을 데드락이 발생하지 않도록 합니다.</li>
      <li>회복: 교착상태가 발생할 때, 해결합니다.</li>
      <li>무시: 회복과정의 성능저하가 심하다면 그냥 무시합니다.</li>
    </ul>
  </p>
  <p>기아상태(Starvation): 여러 프로세스가 부족한 자원을 점유하기 위해 경쟁할 때, 특정 프로세스가 영원히 자원 할당이 되지 않는 경우입니다.</p>
  <p>우선순위를 변경합니다.(우선순위를 수시로 변경하거나, 오래 기다린 프로세스의 우선순위를 높여주거나, Queue를 사용합니다.)</p>
</details>

<details>
  <summary>세마포어와 뮤텍스의 차이에 대해 설명해보세요.</summary>
  </br>
  <p>세마포어는 여러개의 프로세스가 접근 가능한 공유자원을 관리하는 방식이고, 뮤텍스가 될 수 있지만, 뮤텍스는 한 번에 한 개의 프로세스만 접근 가능하도록 관리하는 방식입니다. 따라서 뮤텍스는 세마포어가 될 수 없습니다.</p>
  <p>또, 세마포어는 다른 프로세스가 세마포어를 해제할 수 있지만, 뮤텍스는 락을 획득한 프로세스만 락을 반환할 수 있습니다.</p>
</details>

<details>
  <summary>가상 메모리에 대해 설명해보세요.</summary>
  </br>
  <p>가상 메모리는 프로세스가 실제 메모리의 크기와 상관없이 메모리를 이용할 수 있도록 지원하는 기술 입니다.</p>
  <p>가상 메모리는 실제 메모리(RAM, main memory, first storage)와 보조 기억 장치(auxiliary storage, secondary storage)의 Swap 영역으로 구성됩니다.</p>
  <p>OS 는 메모리 관리자(Memory Management Unit)를 통해 메모리를 관리하며 프로세스는 사용하는 메모리가 실제 메모리인지, Swap 영역인지 모릅니다.</p>
  </br>
  <p>Java 에서는 Swap 영역을 잡아주지 않은 경우 OOM 이 발생할 수 있습니다.</p>
  <p>Swap 영역은 실제 메모리가 아니기 때문에 지연시간이 많이 발생하며, 가급적이면 Swap 메모리를 사용하지 않도록 설계하는 것이 좋고, 만약 계속해서 사용하는 양이 증가한다면 메모리 누수를 의심해 볼 수 있습니다.</p>
</details>

<details>
  <summary>캐시의 지역성에 대해 설명해보세요.</summary>
  </br>
  <p>캐시가 무엇인지, 왜 캐시를 사용하는지를 알고 있어야 합니다. 관련한 좋은 글을 링크해둡니다. https://parksb.github.io/article/29.html</p>
  <p>시간 지역성과 공간 지역성으로 나눌 수 있으며, 시간 지역성은 최근에 접근한 데이터에 다시 접근하는 경향을 의미하고, 공간 지역성은 최근 접근한 데이터의 주변 공간에 다시 접근하는 경향을 의미합니다.</p>
</details>

<details>
  <summary>프로세스 관련 용어를 설명해보세요. (알아만 둡시다.)</summary>
  </br>
  <p>PCB: 프로세스 제어 블록, 프로세스에 대한 중요한 정보를 저장합니다.</p>
  <p>PC: 프로그램 카운터, 프로세스 실행을 위한 다음 명령의 주소를 표시합니다.</p>
  <p>캐시메모리: 자주 사용되는 데이터가 저장되는 공간으로 CPU의 레지스터와 메모리 사이에서 병목 현상을 완화하는 장치입니다.</p>
</details>

### 데이터베이스

<details>
  <summary>데이터베이스에서 인덱스를 사용하는 이유 및 장단점에 대해 설명해주세요.</summary>
  </br>
  <p>데이터베이스에서 인덱스를 사용하는 이유는 검색성능을 향상시키기 위함입니다.</p>
  <p>하지만 검색성능을 실질적으로 향상시키기 위해서는 해당 쿼리가 index를 사용하는지, 카디널리티, Selectivity 같은 요소들이 고려된 인덱스가 생성되어야 합니다.</p>
  <p>일반적인 경우의 장점으로는 빠른 검색 성능을 들 수 있습니다.</p>
  <p>일반적인 경우의 단점으로는 인덱스를 구성하는 비용 즉, 추가, 수정, 삭제 연산시에 인덱스를 형성하기 위한 추가적인 연산이 수행됩니다.</p>
  <p>따라서, 인덱스를 생성할 때에는 트레이드 오프 관계에 놓여있는 요소들을 종합적으로 고려하여 생성해야합니다.</p>
  <p>그렇다고 모든 곳에서 인덱스를 사용하면 오히려 악효과를 낼 수 있다.</p>
  <p>1. 인덱스를 생성하면 추가적인 저장공간이 필요하고 인덱스 관리를 위한 오버헤드가 발생 할 수 있다.</p>
  <p>2. 인덱스가 존재하는 경우, 데이터 삽입,수정,삭제시에도 인덱스가 함께 업데이트 된다. 다라서 인덱스 수가 많이잘수록 쓰기 성능이 감소 할 수 있다.</p>
  <p>3. 쿼리에 사용되지 않는 인덱스가 존재하면, 해당 인덱스는 시스템 리소스 공간을 불필요하게 차지하기 때문에 시스템 전체 성능에 부정적인 영향이 있을 수 있다.</p>
  <p>4. 인덱스를 관리하는것도 비용이 드는 작업이기 때문에 인덱스가 많아지면 관리하기 어려울 수 있다.</p>
  <p>등의 문제가 있기 때문에 인덱스를 생성전에 충분한 분석 및 검토가 필요하여 시스템을 균형있게 유지해야 한다.
  </p>

</details>

<details>
  <summary>트랜잭션에 대해서 설명해주세요.</summary>
  </br>
  <p>트랜잭션이란 데이터베이스의 상태를 변화시키는 하나의 논리적인 작업 단위라고 할 수 있으며, 트랜잭션에는 여러개의 연산이 수행될 수 있습니다.</p>
  <p>트랜잭션은 수행중에 한 작업이라도 실패하면 전부 실패하고, 모두 성공해야 성공이라고 할 수 있습니다.</p>
</details>

<details>
  <summary>ACID에 대해서 설명해주세요.</summary>
  </br>
  <p>ACID는 트랜잭션이 안전하게 수행된다는 것을 보장하기 위한 성질입니다.</p>
  <p>
    <ul>
      <li>Atomicity(원자성): 트랜잭션의 연산은 모든 연산이 완벽히 수행되어야 하며, 한 연산이라도 실패하면 트랜잭션 내의 모든 연산은 실패해야 합니다.</li>
      <li>Consistency(일관성): 트랜잭션은 유효한 상태로만 변경될 수 있습니다.</li>
      <li>Isolation(고립성): 트랜잭션은 동시에 실행될 경우 다른 트랜잭션에 의해 영향을 받지 않고 독립적으로 실행되어야 합니다.</li>
      <li>Durability(내구성): 트랜잭션이 커밋된 이후에는 시스템 오류가 발생하더라도 커밋된 상태로 유지되는 것을 보장해야 합니다. (일반적으로 비휘발성 메모리에 데이터가 저장되는 것을 의미)</li>
    </ul>
  </p>
</details>

<details>
  <summary>트랜잭션 격리 수준(Transaction Isolation Levels)에 대해서 설명해주세요.</summary>
  </br>
  <p>트랜잭션 격리수준은 고립도와 성능의 트레이드 오프를 조절합니다.</p>
  <p>
    <ul>
      <li>READ UNCOMMITTED: 다른 트랜잭션에서 커밋되지 않은 내용도 참조할 수 있다.</li>
      <li>READ COMMITTED: 다른 트랜잭션에서 커밋된 내용만 참조할 수 있다.</li>
      <li>REPEATABLE READ: 트랜잭션에 진입하기 이전에 커밋된 내용만 참조할 수 있다.</li>
      <li>SERIALIZABLE: 트랜잭션에 진입하면 락을 걸어 다른 트랜잭션이 접근하지 못하게 한다.(성능 매우 떨어짐)</li>
    </ul>
  </p>
</details>

<details>
  <summary>정규화에 대해서 설명해주세요.</summary>
  </br>
  <p>정규화는 데이터의 중복방지, 무결성을 충족시키기 위해 데이터베이스를 설계하는 것을 의미합니다.</p>
  <p>이 이상을 물어보는 경우가 있었는데, 학습이 좀 더 필요한 것 같습니다.</p>
</details>

<details>
  <summary>JOIN에 대해서 설명해주세요.</summary>
  </br>
  <p>단순히 SQL에서 JOIN 쿼리가 어떤식으로 동작하는지 알고 있어야 합니다.</p>
  <p>다이어그램으로 이해하는 편이 좋습니다.</p>
</details>

<details>
  <summary>RDBMS vs NOSQL에 대해서 설명해주세요.</summary>
  </br>
  <p>RDBMS는 데이터베이스를 이루는 객체들의 릴레이션을 통해서 데이터를 저장하는 데이터베이스입니다. SQL을 사용해 데이터의 저장, 질의, 수정, 삭제를 할 수 있으며 데이터를 효율적으로 보관하는 것을 목적으로 하고 구조화가 굉장히 중요합니다.</p>
  <p>장점으로는 명확한 데이터 구조를 보장하고, 중복을 피할 수 있습니다.</p>
  <p>NOSQL은 RDBMS에 비해 자유로운 형태로 데이터를 저장합니다. 또한 수평확장을 할 수 있고 분산처리를 지원합니다. 다양한 형태의 NOSQL 데이터베이스가 있고, 대표적으로 key-value store, bigtable, dynamo, document db, graph db 등이 있습니다.</p>
  <p>둘은 대체될 수 있는 것이 아니고, 각각 필요한 시점에 적절히 선택해서 사용해야 합니다. 둘 다 같이쓰는 상호보완적인 존재가 될 수도 있습니다.</p>
</details>

<details>
  <summary>Redis에 대해서 간단히 설명해주세요.</summary>
  </br>
  <p>Redis는 key-value store NOSQL DB입니다. 싱글스레드로 동작하며 자료구조를 지원합니다. 그리고 다양한 용도로 사용될 수 있도록 다양한 기능을 지원합니다. 데이터의 스냅샷 혹은 AOF 로그를 통해 복구가 가능해서 어느정도 영속성도 보장됩니다.</p>
  <p>스프링에서는 세션을 관리하거나, 캐싱을 하는데에 자주 사용되는 것으로 알고 있습니다.</p>
</details>

<details>
  <summary>Redis와 Memcached의 차이에 대해서 설명해주세요.</summary>
  </br>
  <p>Redis는 싱글 스레드 기반으로 동작하고, Memcached는 멀티스레드를 지원해서 멀티 프로세싱이 가능합니다.</p>
  <p>Redis는 다양한 자료구조를 지원하고, Memcached는 문자열 형태로만 저장합니다.</p>
  <p>Redis는 여러 용도로 사용할 수 있도록 다양한 기능을 지원합니다.</p>
  <p>Redis는 스냅샷, AOF 로그를 통해서 데이터 복구가 가능합니다.</p>
</details>

<details>
  <summary>Elastic Search에 대해서 간단히 설명해주세요.</summary>
  </br>
  <p>Elastic Search는 자바로 개발된 오픈소스 검색엔진 입니다. 보통 단독으로 사용하기보다는 ELK 스택이라고 부르는 Logstash, Kibana, Beats를 추가적으로 사용합니다.</p>
  <p>Inverted Index 구조로 데이터를 저장해서, 전문(Full-text) 검색시에 RDBMS에 비해 뛰어난 성능을 보장합니다.</p>
  <p>다양한 용도로 사용할 수 있습니다. (데이터 저장, 문서 검색, 위치 검색, 머신 러닝 기반 검색, 로그 분석, 보안 감사 분석 등)</p>
</details>

<details>
  <summary>Elastic Search의 인덱스구조와 RDBMS의 인덱스 구조의 차이에 대해 설명해주세요.</summary>
  </br>
  <p>Elastic Search는 Inverted-Index 구조로 데이터를 저장합니다. 이는 책의 색인을 생각해보면 쉬운데, 특정 단어가 출현하는 doc을 저장하는 것입니다. 반면 RDBMS는 B-Tree와 그와 유사한 인덱스를 사용합니다. 데이터가 어디에 존재하는지 어떤 순서로 저장하는 지의 차이라고 생각합니다. RDBMS에도 다양한 인덱스 구조가 있으나 여기서 예로 든 것은 B-Tree 인덱스입니다.</p>
</details>

<details>
  <summary>Elastic Search의 키워드 검색과 RDBMS의 LIKE 검색의 차이에 대해 설명해주세요.</summary>
  </br>
  <p>Elastic Search의 키워드 검색은 document를 저장할 때 수행하는 알고리즘과 동일한 알고리즘으로 키워드를 분리합니다. 그 중에서 랭킹알고리즘을 통해서 가장 유사한 순서대로 결과를 나타냅니다.</p>
  <p>RDBMS에서의 LIKE 검색은 와일드카드로 시작하지 않는 경우에만 인덱스를 사용하고 나머지 경우는 전체를 탐색하기 때문에 상대적으로 느립니다.</p>
</details>

<details>
  <summary>MongoDB에 대해서 간단히 설명해주세요.</summary>
  </br>
  <p></p>
</details>

<details>
  <summary>CAP 이론과, Eventual Consistency에 대해서 설명해주세요.</summary>
  </br>
  <p>CAP 이론은 분산 환경에서 모두를 만족하는 시스템은 없다는 이론입니다.</p>
  <p>
    <ul>
      <li>Consitenty(일관성): ACID의 일관성과는 약간 다릅니다. 모든 노드가 같은 시간에 같은 데이터를 보여줘야 한다는 것입니다.</li>
      <li>Availability(가용성): 모든 동작에 대한 응답이 리턴되어야 합니다.</li>
      <li>Partition Tolerance(분할 내성): 시스템 일부가 네트워크에서 연결이 끊기더라도 동작해야 합니다.</li>
    </ul>
  </p>
  <p>CAP는 해당 시스템이 이거다 하고 말하기 곤란한게 어떻게 클러스터링 하느냐에 따라 달라질 수 있습니다. 그렇기 때문에 어떤 전략을 취할 때 어떤 것을 선택했는가를 잘 알아야 합니다. (단순히 MySQL이 CA입니다. 보다는 어떤 이유로 CA인지 근거를 생각해보기) 그리고 어느정도 한계가 있는 이론이고 PACELC 이론이라고 또 있습니다.</p>
  <p>Eventual Consistency는 이 Consistency를 보장해주지 못하기 때문에 나온 개념으로, Consistency를 완전히 보장하지는 않지만, 결과적으로 언젠가는 Conssistency가 보장됨을 의미합니다.</p>
</details>

