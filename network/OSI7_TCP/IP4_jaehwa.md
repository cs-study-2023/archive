## OSI 7계층

OSI 7계층 모델은 네트워크 통신이 일어나는 과정을 7단계로 나눈 것을 말한다. 계층을 이렇게 나눈 이유는 통신이 일어나는 과정을 단계별로 파악하기 용이하고 어느 특정 계층에 이상이 생겼을 때 다른 계층은 놔두고 문제가 있는 계층만 고쳐서 문제를 해결할 수 있다.

> **(It is because of the fact that it will be easy for troubleshooting the network problems.**
> 
> 
> Only the layer in which the problem exist will be modified. Other layers are left untouched.)
> 

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/fb38e82c-61f0-4aa9-b785-e0a798e9b9df/e709740a-1425-471a-b9cb-20166c74c025/Untitled.png)

1. **물리 계층(Physical Layer)**
    
    1계층은 전기적, 기계적, 기능적인 특성을 이용해 데이터를 전송하는 역할을 담당합니다. 이 때 사용되는 데이터의 단위는 '비트'로, 이는 전기적으로 On과 Off, 즉 1과 0으로 표현됩니다. 이 계층은 데이터의 내용이나 에러 여부 등을 확인하지 않고, 단순히 데이터를 전기적인 신호로 변환하여 전송하는 역할만 합니다. 이 계층에서 사용되는 대표적인 기기는 통신 케이블, 리피터, 허브 등입니다.
    
    → 물리계층은 통신 케이블, 리피터, 허브 등을 통해 데이터를 전기적 신호로 변환하고 전송하는 역할을 합니다.
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/fb38e82c-61f0-4aa9-b785-e0a798e9b9df/11c89cee-7b75-4a71-8f1b-d816e3068906/Untitled.png)
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/fb38e82c-61f0-4aa9-b785-e0a798e9b9df/44edb48f-adce-4527-b4a9-476f6cebd2ee/Untitled.png)
    
2. **데이터 링크 계층(DataLink Layer)**
    
    2계층은 물리계층을 통해 송수신되는 정보의 오류와 흐름을 관리하며, 안전한 정보 전달을 보장하는 역할을 합니다. 이 계층에서는 맥 주소를 사용하여 통신하며, '프레임'이라는 단위로 데이터를 전송합니다. 브리지나 스위치와 같은 장비가 대표적으로 이 계층에서 작동합니다.
    
    데이터 링크계층은 오류 제어와 흐름 제어를 위해 CRC 기반의 메커니즘을 사용하며, 물리계층에서 발생할 수 있는 오류를 찾아내고 수정하는 역할을 합니다.
    
    맥 주소는 네트워크 카드가 생성될 때부터 할당되며, 이 계층의 주소 체계는 계층이 없는 단일 구조입니다. 이더넷, HDLC, ADCCP 등의 포인트 투 포인트 프로토콜, 그리고 패킷 스위칭 네트워크나 LLC, ALOHA 같은 근거리 네트워크용 프로토콜 등이 이 계층에서 사용됩니다.
    
    → 데이터 링크계층은 브리지나 스위치를 사용하여 오류 검출, 재전송, 흐름 제어를 수행하고, 프레임에 맥 주소를 부여하여 안전한 정보 전달을 보장합니다.
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/fb38e82c-61f0-4aa9-b785-e0a798e9b9df/7b025fc6-60d4-4c06-a408-ce799d08faaf/Untitled.png)
    
3. **네트워크 계층(Network Layer)**
    
    데이터를 목적지까지 가장 안전하고 빠르게 전달하는 역할을 담당합니다. 이를 위해 경로를 선택하고 주소를 지정하며, 그 경로에 따라 패킷을 전달하는 역할을 수행합니다. 이 계층에서 동작하는 대표적인 장비로는 라우터가 있으며, IP 주소가 사용됩니다.
    
    또한, 이 계층은 여러 노드를 거칠 때마다 경로를 찾아주는 역할을 수행하며, 다양한 길이의 데이터를 여러 네트워크를 통해 전달하는 역할도 담당합니다. 이 과정에서 전송 계층이 요구하는 서비스 품질(QoS)을 제공하기 위한 기능적, 절차적 수단을 제공합니다.
    
    네트워크 계층은 라우팅, 흐름 제어, 세그멘테이션, 오류 제어 등의 역할을 수행합니다. 데이터를 연결하는 다른 네트워크를 통해 전달함으로써 인터넷이 가능하게 만드는 계층이기도 합니다. 이 계층에서는 네트워크 관리자가 직접 할당하는 논리적인 주소 구조(IP)를 사용하며, 이는 계층적입니다.
    
    마지막으로, 이 계층은 서브네트의 최상위 계층으로서 경로를 설정하고, 청구 정보를 관리합니다. 개방형 시스템 간에 네트워크 연결을 설정, 유지, 해제하는 기능을 부여하며, 전송 계층 사이에 네트워크 서비스 데이터 유닛(NSDU)을 교환하는 기능을 제공합니다. 따라서 이 계층의 주요 역할은 주소 부여(IP)와 경로 설정(Route)입니다.
    
    **IP 계층**
    
    IP 계층은 TCP/IP 프로토콜에서 네트워크의 주소 (IP 주소)를 정의하고, IP 패킷의 전달 및 라우팅을 담당하는 계층입니다. OSI 7계층 모델의 관점에서는 네트워크 계층에 해당하며, 패킷을 목적지까지 전달하는 역할을 수행합니다. 이는 하위계층인 데이터링크 계층의 하드웨어적인 특성에 관계없이 독립적으로 수행됩니다.
    
    IP 계층에서 주요 프로토콜로는 패킷의 전달을 책임지는 IP, 패킷 전달 에러의 보고 및 진단을 위한 ICMP, 그리고 복잡한 네트워크에서 인터네트워킹을 위한 경로를 찾게 해주는 라우팅 프로토콜 등이 있습니다.
    
    **IP 프로토콜**
    
    TCP/IP 기반의 인터넷 망을 통하여 데이타그램의 전달을 담당하는 프로토콜
    
4. **전송 계층(Transport Layer)**
    
    통신을 활성화하는 계층으로, 주로 TCP 프로토콜을 이용합니다. 이 계층에서는 포트를 열어 응용 프로그램들이 데이터를 전송할 수 있게 합니다. 데이터가 도착하면 이 계층에서 데이터를 하나로 합쳐 상위 계층에 전달합니다. 이 계층의 주요 역할로는 단대단 오류제어 및 흐름제어가 있으며, TCP/UDP 프로토콜을 사용합니다.
    
    전송 계층은 양 끝단 사용자들이 신뢰성 있는 데이터를 주고받을 수 있게 해주며, 상위 계층들이 데이터 전달의 유효성이나 효율성을 고려하지 않도록 합니다. 주로 시퀀스 넘버 기반의 오류 제어 방식을 사용하며, 일부 프로토콜은 상태 개념을 가지고 있고 연결 기반입니다. 이 계층에서는 패킷들의 전송이 유효한지 확인하고 전송 실패한 패킷들을 다시 전송합니다.
    
    TCP 프로토콜은 전송 계층에서 사용되는 연결지향적이고 신뢰성 있는 프로토콜로, 패킷 손실, 중복, 순서 바뀜 등을 방지해줍니다. TCP는 연결 관리를 위한 연결 설정 및 연결 해제가 필요하며, 양단간 어플리케이션/프로세스는 TCP가 제공하는 연결성 회선을 통해 서로 통신합니다.
    
    반면에, UDP 프로토콜은 비연결성이며 신뢰성이 없어, 실시간 응용이나 빠른 요청과 응답이 필요한 경우에 적합합니다. UDP는 데이터그램 지향의 전송계층용 프로토콜로, 헤더 처리에 많은 시간과 노력을 요하지 않습니다. 이 프로토콜은 실시간 응용 및 멀티캐스팅이 가능하며, 헤더는 단순하게 구성되어 있습니다.
    
5. **세션 계층(Session Layer)**
    
    데이터가 통신하기 위한 논리적인 연결을 담당하는 계층입니다. 이 계층은 통신을 위한 '대문' 역할을 하며, 세션 설정, 유지, 종료, 전송 중단 시 복구 등의 기능을 수행합니다. 하지만 4계층에서도 연결을 맺고 종료할 수 있어서 어느 계층에서 통신이 끊어졌는지 판단하기는 한계가 있습니다. 따라서 세션 계층은 4 계층과 무관하게 응용 프로그램 관점에서 봐야 합니다.
    
    세션 계층은 양 끝단의 응용 프로세스가 통신을 관리하는 방법을 제공합니다. 이 계층에서는 동시 송수신 방식(duplex), 반이중 방식(half-duplex), 전이중 방식(full duplex)의 통신과 함께, 체크 포인팅과 유효, 종료, 다시 시작 과정 등을 수행합니다. 이 계층은 TCP/IP 세션을 만들고 없애는 책임을 지닙니다.
    
    세션 계층의 주요 역할로는 통신하는 사용자들을 동기화하고 오류 복구 명령들을 일괄적으로 다루는 것이 있습니다. 이 계층에서는 통신을 하기 위한 세션을 확립, 유지, 중단하는 역할을 수행합니다.
    
6. **표현 계층(Presentation Layer)**
    
    데이터 표현에 대한 독립성을 제공하고 암호화를 담당하는 계층입니다. 이 계층은 코드 간의 번역을 담당하여 사용자 시스템에서 데이터 형식의 차이를 처리하는 부담을 덜어줍니다. 예를 들어, EBCDIC로 인코딩된 문서 파일을 ASCII로 인코딩된 파일로 변환하거나, 데이터가 TEXT인지 그림인지, GIF인지 JPG인지 구분하는 일이 이 계층에서 이루어집니다. 이 외에도 MIME 인코딩이나 암호화 등의 작업이 이루어집니다.
    
7. **응용 계층(Application Layer)**
    
    최종 목적지로, 이 계층에서는 HTTP, FTP, SMTP, POP3, IMAP, Telnet 등의 프로토콜이 사용되며, 이 프로토콜들은 통신 패킷을 처리합니다. 응용 계층은 사용자가 프로토콜을 더 쉽게 사용할 수 있도록 도와주는 응용 프로그램이 있습니다. 이 계층은 응용 프로세스와 직접 관계를 맺어 일반적인 응용 서비스를 수행하며, 관련된 응용 프로세스들 사이의 전환을 제공합니다.
    

## TCP/IP 4계층

TCP/IP는 실제 인터넷 표준을 나타내는 4계층 모델로, 데이터 전송 표준인 OSI 7계층을 실제로 구현한 것입니다. 이는 2개의 주요 프로그램, 즉 상위 계층인 TCP와 하위 계층인 IP로 구성되어 있습니다.

TCP(Transmission Control Protocol)는 메시지나 파일들을 작은 패킷으로 나누어 인터넷을 통해 전송하고, 수신된 패킷들을 원래의 메시지로 재조립하는 역할을 합니다.IP(Internet Protocol)는 각 패킷의 주소 부분을 처리하여 패킷들이 목적지에 정확하게 도달할 수 있게 합니다.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/fb38e82c-61f0-4aa9-b785-e0a798e9b9df/3887793d-ce12-4dd1-a001-eea3f1d44475/Untitled.png)

TCP/IP의 네 가지 계층은 다음과 같습니다:

**네트워크 인터페이스 계층(Network Interface Layer)**

OSI 계층의 1,2 계층에 해당하며, TCP/IP 패킷을 네트워크 매체로 전달하고, 네트워크 매체에서 TCP/IP 패킷을 수신하는 역할을 합니다. 에러 검출 기능과 패킷의 프레임화 기능을 수행합니다.

**인터넷 계층(Internet Layer)**

OSI 계층의 3계층에 해당하며, 어드레싱, 패키징, 라우팅 기능을 제공합니다. 논리적 주소인 IP를 이용한 노드간 전송과 라우팅 기능을 처리합니다.

**전송 계층(Transport Layer)**

OSI 계층의 3,4 계층에 해당하며, 자료의 송수신을 담당합니다. TCP와 UDP가 핵심 프로토콜로, 데이터의 제어 정보가 이 계층에 포함됩니다.

**응용 프로그램 계층(Application Layer)**

다른 계층의 서비스에 접근할 수 있게 하는 어플리케이션을 제공합니다. TCP/IP 네트워크를 사용하거나 관리하는 것을 도와주는 프로토콜이 이 계층에 포함됩니다.

---
### 예상 질문
1. OSI 계층에는 어떤 계층들이 존재하나요?
2. (3,4 계층이 중요한 거 같음) 두 계층에 대해 말해주세요.
3. TCP/IP 4계층은 osi와 비교했을 때 어떤 계층들로 이뤄졌나요.

---

### 참고 링크

[OSI 7 계층이란?, OSI 7 계층을 나눈 이유](https://shlee0882.tistory.com/110)

[[네트워크] OSI 7계층, TCP/IP 4계층 모델](https://devowen.com/344)

[TCP/IP 4계층](https://tar-cvzf-studybackup-tar-gz.tistory.com/38)