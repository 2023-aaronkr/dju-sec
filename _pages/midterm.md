---
layout: page
title: Midterm Guide / 중간고사 가이드
permalink: /midterm/
---

{:toc}

---

<style>
table {
  border: 1px solid gainsboro;
  border-bottom: none;
  border-collapse: collapse;
  min-width: 80%;
}
th, td {
  border-bottom: 1px solid gainsboro;
  padding: 10px;
}
th {
  background-color: lightslategray;
  color: white;
}
td:first-child {
  background-color: whitesmoke;
}
</style>

**주제**

1. [웹사이트를 해킹하다](#1-웹사이트를-해킹하다)
2. [인터넷 작동 방식](#2-인터넷-작동-방식)
3. [브라우저 작동 방식](#3-브라우저-작동-방식)
4. [웹 서버 작동 방식](#4-웹-서버-작동-방식)

**코딩**

1. [Node.js의 이해 / 시작하기](#1-nodejs의-이해--시작하기)
2. [첫 번째 Node.js 웹 서버 만들기](#첫-번째-nodejs-웹-서버-만들기)

---

## 주제

**들어가며**

해킹이 가장 자주 발생하는 곳:

- Windows: 윈도우는 컴퓨터 바이러스의 주요 표적이었고, 인터넷은 효과적인 전달 메커니즘을 증명했다.
- Microsoft의 ActiveX: 마이크로소프트는 웹을 ‘소유’하려는 시도로 액티브XActiveX 와 같은 독점 기술을 브라우저에 도입했다. 불행히도 액티브X 때문에 멀웨어 malware가 증가했는데 이는 사용자의 기계를 감염시키는 악성 소프트웨어다.
- Web Browser와 JavaScript: 해커들은 크로스 사이트 스크립팅 XSS, Cross-Site Scripting 공격으로 자바스크립트 코드를 페이지에 주입하는 방법을 찾았으며, 인터넷은 훨씬 더 위험한 장소가 됐다.
- PHP 및 동적 웹사이트: PHP는 PHP 런타임 엔진으로 공급될 수 있는 임베디드 처리 태그가 있는 HTML이라는 템플릿 파일의 개념을 대중화했다. 동적dynamic PHP 웹사이트(페이스북의 초기 화신처럼)는 인터넷으로 번창했다. 그러나 동적 서버 코드는 완전히 새로운 보안 취약 범주를 도입했다.
- Web Server: 해커들은 인젝션Injection 공격을 이용해서 서버에 악성 코드를 실행하거나 디렉터리 접근 공격을 사용해서 서버의 파일 시스템을 탐색하는 새로운 방법을 발견했다.
- IoT: 자동차, 초인종, 냉장고, 전구, 고양이 쟁반과 같은 인터넷을 활성화히는· 일상 기기의 추세는 공격의 새로운 벡터를 열었다. 사물인터넷에 연결하는 어플라이언스appliance가 간단할수록 보안 기능이 자동으로 업데이트되지 않는다.
- Hacking: 이로 인해 안전하지 않은 수많은 인터넷 노드가 도입돼 해커가 원격으로 설치하고 제어할 수 있는 악성 소프트웨어 에이전트인 봇넷botnet에 풍부한 호스팅 환경을 제공한다.

- 여전히 10년 전에 처음 발견된 보안 문제를 해결하고 있으며, 그렇기 때문에 이 책에서는 웹사이트에 영향을 미칠 수 있는 모든 주요 보안 결함을 설명한다.

가장 일반적인 보안 취약점을 배워 차단하는 방법을 안다면 99%의 공격에서 시스템을 보호할 수 있다.

**Security Slides**

Phishing is a type of social engineering attack often used to steal user data, including login credentials and credit card numbers. / 피싱은 로그인 자격 증명 및 신용 카드 번호를 포함한 사용자 데이터를 도용하는 데 자주 사용되는 사회 공학 공격 유형입니다.

Hacking is a term used to describe actions taken by someone to gain unauthorized access to a computer. / 해킹은 누군가가 컴퓨터에 무단으로 액세스하려는 시도를 설명하는 데 사용되는 용어입니다.

Password Security is a set of rules designed to protect the secrecy of passwords. / 비밀번호 보안은 비밀번호의 비밀을 보호하기 위해 설계된 규칙의 집합입니다.

Social Engineering is the art of manipulating people so they give up confidential information. / 사회 공학은 사람들을 조작하여 기밀 정보를 제공하도록 하는 기술입니다.

### 1. 웹사이트를 해킹하다

1 장에서는 해커들이 어떻게 공격하는지 그리고 해킹을 시작 히는 것이 얼마나 쉬운지를 보여 준다.

- White hat hacker: 좋은 해커들은 재미로 보안 허점을 찾으려고 노력하며, 소프트웨어 판매업자와 웹사이트 소유자들에게 익스플로엇을 공개하기 전에 취약점들을 알려 준다.
- Black hat hacker: 윤리 의식이 낮은 블랙 해커들 black hacker 은취약점을 이용할수 있는시간대를극대화하려고 익스플로잇 코드를 쌓거나 비트코인 블랙마켓에서 익스플로잇 코드를 팔기도 한다.
- Gray hat hacker: 그레이 해커들 gray hacker 은 보안 결함을 찾아내는 것에 대해 돈을 받지만, 익스플로잇을 공개하기 전에 소프트웨어 판매업자와 웹사이트 소유자들에게 알려주지 않는다.
- Zero-day exploit: 제로 데이 익스플로잇: 공개된 지 하루도 안 되거나 아예 공개되지 않은 익스플로엇
- patch: 패치: 소프트웨어 판매업자가 보안 결함을 수정하는 코드 조각
- exploit: 해킹 커뮤니티에서는 보안 결함을 이용하는 코드 조각fragment을 익스플로잇 exploit 이라고 부른다.
- Kali Linux: 칼리 리눅스는 해킹에 사용되는 운영 체제로, 해킹 도구를 설치하고 실행하는 데 필요한 모든 것을 제공한다.
- Metasploit: 메타스플로잇은 해킹 도구의 모음으로, 웹사이트를 해킹하는 데 사용할 수 있는 수많은 익스플로잇을 포함한다.

[목차로 돌아가기](#midterm-guide--중간고사-가이드)

---

### 2. 인터넷 작동 방식

- ARPANET: 인터넷은 1969년에 ARPANET으로 시작했다. ARPANET은 미국 국방부의 고등 연구 기획국 ARPA, Advanced Research Projects Agency가 개발한 네트워크로, 미국의 대학과 연구소를 연결했다.
- Data representation: 데이터 표현: 컴퓨터는 0과 1로 이루어진 비트bit의 시퀀스sequence로 모든 것을 표현한다.
- bit: 비트: 컴퓨터는 0과 1로 이루어진 비트bit의 시퀀스sequence로 모든 것을 표현한다.
- byte: 바이트: 8개의 비트로 구성된 바이트byte는 컴퓨터에서 가장 일반적으로 사용되는 데이터 단위다.
- Internet protocol suite: 인터넷 프로토콜 스위트: 인터넷 프로토콜 스위트는 인터넷에서 데이터를 전송하는 데 사용되는 프로토콜의 모음이다.
- TCP (Transmission Control Protocol): TCP(전송 제어 프로토콜): 모든 패킷이 수신되고 올바르게 순서가 지정되었는지 확인하기 위해 오류 검사를 수행하는 패킷 전송용 프로토콜입니다.
- packet: 패킷: 네트워크를 통해 전송되는 데이터 덩어리입니다. 더 큰 메시지는 대상에 순서대로, 순서대로 도착하지 않거나 전혀 도착하지 않을 수 있는 패킷으로 나뉩니다.
- packet metadata: 패킷 메타데이터: 네트워크를 통해 패킷을 라우팅하고 원본 메시지를 재구성하는 데 도움이 되도록 패킷에 추가된 데이터입니다.
- Datastream: 데이터스트림(Datastream): 인터넷을 통해 패킷으로 전달되는 정보입니다.
- UDP (User Datagram Protocol): UDP(사용자 데이터그램 프로토콜): 오류 확인을 최소화하고 삭제된 패킷을 재전송하지 않고 빠르게 패킷을 전송하기 위한 프로토콜.

|                       | UDP (사용자 데이터그램 프로토콜)                                                                               | TCP (전송 제어 프로토콜)                                                                                                                       |
| --------------------- | -------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| 주요 아이디어         | 가능한 한 빨리 도서관을 정리하는 것과 같습니다. 정확성을 걱정하지 않고 신속하게 정보를 보내는 것이 목표입니다. | 도서관에 있는 모든 책에 번호를 매기는 것과 같습니다. 속도는 느리지만 더 정확합니다.                                                            |
| 작동 방식의 기본 사항 | 모든 패킷을 보내되 모든 패킷이 올바른 순서로 통과하거나 도착하는지 확인하지 마십시오.                          | 패킷을 다시 정렬할 수 있도록 번호를 매기고, 모두 수신되었는지 확인하고, 누락된 패킷을 다시 보냅니다. 발신자와 수신자 간의 여러 번의 앞뒤 확인. |
| 실생활에서의 활용     | 화상 회의, 라이브 스트리밍, 온라인 게임 등 오류 수정보다 짧은 시간이 더 중요한 경우에 유용합니다.              | 이메일이나 사진을 보내거나 웹사이트를 탐색하는 등 찰나의 순간을 절약하는 것보다 정확성이 더 중요한 경우에 유용합니다.                          |

- IP (Internet Protocol): 인터넷상의 데이터 패킷은 인터넷 프로토콜 IP (Internet Protocol) 주소로 전송되며, 개별 인터넷에 연결된 컴퓨터에 할당된 번호로 전송한다.
- ICANN (Internet Corporation for Assigned Names and Numbers): 국제 도메인 관리 기구 ICANN, (Internet Corporation for Assigned Names and Numbers)는 가장 높은 수준에서 지역 당국에 IP 주소의 블록을 할당한다.
- ISP (Internet Service Provider): 지역 당국은 인터넷 서비스 제공업체 ISP, Internet Service Provider와 해당 지역 내 호스팅 회사에 주소 블록을 부여한다.
- IPv4: IP 주소는 이진수로 일반적으로 232(4,294,967,296) 주소를 허용하는 1P 버전 4(IPv4) 구문으로 작성되며,
- IPv6: IPv4 주소가 지속 가능하지 않은 속도로 사용되고 있기 때문에 콜론으로 구분된 4개의 16진수 숫
  자의 8개 그룹

**IPv4**

**IPv6**

IPv6 주소 단축

1. 규칙 1: 모두 0인 그룹을 생략합니다.
2. 규칙 2: 선행 0 생략
3. 규칙 1과 2 결합

- DNS (Domain Name System): 웹사이트 주소를 사용자에게 더 친근하게 만들려고 example.com과 같은 사람이 읽을 수 있는 도메인을 93.184.216.119과 같은 1P 주소로 변환하는 DNS Domain Name System 라는 글로벌 디렉터리를 사용한다.
- Cache: 브라우저가 도메인 이름을 처음 접하게 되면 로컬 도메인 네임 서버(일반적으로 ISP가 호스팅하는 서버)를 사용해 검색한 다음, 결과를 캐시 cache해 향후에 시간이 많이 걸리는 검색을 방지한다.
- 애플리케이션 계층 프로토콜: 애플리케이션 계층 프로토콜은 인터넷 프로토콜 스위트의 일부로, 애플리케이션 간에 데이터를 전송하는 데 사용되는 프로토콜이다.
- HTTP (HyperText Transfer Protocol): (책에서 설명한 모든 익스플로잇은 HTTP를 어떤 식으로든 사용하고 있기 때문에 HTTP 통신을 구성하는 요청과 응답이 어떻게 작동하는지 자세히 알수 있다.)
- HTTP handshake: HTTP 핸드쉐이크: HTTP 요청과 응답은 핸드쉐이크 handshake라고 하는 특정 순서로 전송된다.
- HTTP session: HTTP 세션: HTTP 세션은 HTTP 요청과 응답이 서로 연결된 것을 나타내는 데 사용되는 용어다.
- HTTP cookies: HTTP 쿠키: HTTP 쿠키는 웹사이트가 사용자를 식별하는 데 사용하는 데이터 조각이다.

**HTTP 요청**

1. Method: (GET / POST / PUTS / DELETE)
2. URL (Universal Resource Locator): (https://www.example.com)
3. Headers: (Accept-Language: en-US)
4. Body: (username=abc&password=123)

- Encryption: 암호화: 암호화는 데이터를 암호화하고 복호화하는 데 사용되는 알고리즘을 의미한다.
- TLS (Transport Layer Security): TLS(전송 계층 보안)은 HTTP 요청과 응답을 암호화하는 데 사용되는 프로토콜이다.
- HTTPS (HyperText Transfer Protocol Secure): HTTPS(보안 HTTP)는 TLS를 사용하는 HTTP의 보안 버전이다.

[목차로 돌아가기](#midterm-guide--중간고사-가이드)

---

### 3. 브라우저 작동 방식

- Web rendering pipeline: 웹 렌더링 파이프라인: 브라우저는 HTML, CSS, 자바스크립트를 사용해 웹사이트를 렌더링한다. 렌더링 파이프라인은 브라우저가 웹사이트를 렌더링하는 방식을 설명한다.
- DOM (Document Object Model): DOM: HTML을 페이지 구성 방식에 대한 브라우저의 이해를 나타내는 메모리 내 데이터 구조.
- CSSOM (CSS Object Model): CSSOM: 일단브라우저가 DOM을 생성하지만화면에 어떤 것을그리기 전에 스타일링 규칙을 각 DOM 요소에 적용해야 한다.
- Javascript: JavaScript: 브라우저는 또한 DOM을 구성할 때 우연히 발견되는 자바스크립트를 로드하고 실행한다. 자바스크립트 코드는 페이지가 렌더링되기 전이나 사용자 행동에 대옹해 DOM과 스타일링 규칙을 동적으로 변경할 수 있다.
- Browser Security model: 브라우저 보안 모델: 브라우저는 웹사이트가 브라우저의 보안 모델을 우회할 수 없도록 보호한다.
- Sandbox: 샌드박스: 브라우저는 웹사이트가 브라우저의 보안 모델을 우회할 수 없도록 보호한다.

**렌더링 전/후: 브라우저에서 수행하는 다른 모든 작업**

브라우저는 렌더링 파이프라인과 자바스크립트 엔진보다 훨씬 더 많다.

HTML 렌더링과 자바스크립트 실행 외에도 현대의 브라우저들은 많은 다른 책임에 대한 논리를 포함하고있다.

- 브라우저는 운영체제와 연결해 DNS 주소를 확인 및 캐시하고,
- 보안 인중서를 해석및 검중하며,
- 필요할 때 HTTPS로 요청을 인코딩하며,
- 웹 서버의 지시에 따라 쿠키를 저장하고 전송한다.

이런 가정들이 어떻게 조화를 이루는지 이해하고자 아마존에 로그인한 사용자의 뒷면을 살펴본다.

**예**

1. Coupang.com 들어가면
2. IP 주소? DNS에서 확인. 없으면 ISP 물어봐
3. TCP 연결하는 핸드쉐크
4. HTTP GET 요청, 패킷 받기
5. HTTPS으로 바꾸고 TLS 핸드쉐크으로 연결
6. 페이지를 구문 분석하고 표시
7. 사용자가 로그인 페이지에서 HTTP POST 메소드 전달
8. 서버가 로그인을 검증하고 Set-Cookie 헤더(지정된 시간 동안 저장됨)를 사용하여 세션을 설정합니다.

[목차로 돌아가기](#midterm-guide--중간고사-가이드)

---

### 4. 웹 서버 작동 방식

- Static resources (sites) 정적 자원: 정적 자원은 HTML 파일, 이미지 파일 또는 웹 서버가 HTTP 응답에서 변경되지 않고 반환하는 다른 유형의 파일이다.
- Dynamic resources (sites) 동적 자원: 동적 자원은 웹 서버가 HTTP요청에 대응해 실행하거나 해석하는 코드, 스크립트 또는 템플릿 template 이다. 대부분의 현대 웹사이트는 동적 자원을 대신 사용한다. 동적 자원의 코드는 종종 HTTP 옹답을 채우려고 데이터베이스에서 데이터를 로드한다.
- CDN (Content Delivery Network): 콘텐츠 전송 네트워크 CDN, Content Delivery Network로, 정적 지원의 중복된 복사본을 전 세계 데이터 센터에 저장하고 가장 가까운 물리적 위치에서 브라우저로 신속하게 전달한다.
- CMS (Content Management System): 여전히 많은 웹사이트가 대부분 정적 콘텐츠로 구성돼 있다. 정적 콘텐츠로 구성된 사이트는 손으로 코딩하기보다는 콘텐츠 작성에 필요한 기술적 지식이 거의 또는 전혀 필요하지 않은 제작 도구를 제공하는 콘텐츠 관리 시스템 CMS, Content Management System을 사용해일반적으로 구축된다.
- Template files: 템플릿은 대부분 HTML이지만, 그 안에 웹 서버에 대한 지시 사항을 포함하는 프로그램적 로직을 갖고 있다. 로직은 일반적으로 간단하며 보통 세 가지 중 하나를 수행한다.

1. 데이터베이스나 HTTP 요청에서 데이터를 끌어와 HTML에 보간하거나
2. HTML 템플릿의 섹션을 조건부로 렌더링하거나
3. 데이터 구조(예: 항목 목록)를 루프해 HTML 블록을 반복 적으로 렌더링한다.

- Database (데이터베이스): 데이터베이스는 데이터를 저장하는 데 사용되는 소프트웨어다. 데이터베이스는 일반적으로 테이블table, 행row, 열column, 인덱스index, 뷰view 등의 데이터 구조를 사용한다.
- SQL (Structured Query Language) "sequel": SQL 데이터베이스는 관계형 relational 이며, 공식적으로 규정된 방식이고, 서로 관련된 하나 이상의 테이불table 에 데이터를 저장한다는 것을 의미한다. 관계형 데이터베이스의 데이터베이스 테이블은 키를 통해 서로 관련돼 있다. 보통 테이블의 각 행에는 고유한 숫자 기본 키 primary key가 있으며, 테이블은 외래키 foreign key로 서로의 행을 나타낼 수 있다.
- NoSQL: NoSQL 데이터베이스는 종종 스키마schema가 없으므로 데이터 구조를 업그레이드하지 않고도 새 레코드에 필드를 추가할 수 있다. 유연성을 얻기 위해 데이터는 키 값key-value 형식이나 자바스크립트 객체 표기법 JSON, JavaScript Object Notation 에 저장되는 게 많다.
- Caching: 캐싱 caching 이란 쉽게 검색할 수 있는 형태로 다른 곳에 보관된 데이터의 복사본을 저장해 데이터의 검색 속도를 높이는 과정을 말한다.

**Web Programming Languages (웹 프로그래밍 언어)**

- 루비온레일즈: (1990) 루비 온 레일즈는 대규모 웹 애플리케이션 구축을 위한 많은 모범 사례를 통합하고 최소한의 구성으로 구현이 용이하다.
- 파이썬: (1980) 깨끗한 구문, 유연한 프로그래밍 패러다임, 다양한 모델들이 파이썬을 인기 있게 만들었다.
  자바스크립트와 Node.js: Node.js는 V8 자바스크립트 엔진 위에서 실행되는데, 구글 크롬이 브라우저 내에서 자바스크립트를 해석하는 데 사용하는 소프트웨어 구성 요소와 동일하다.
- PHP: PHP 언어는 리눅스에서 동적 사이트를 구축하려고 사용되는 C 바이너리 집합에서 개발됐다. PHP는 계획되지 않은 언어의 진화가 체계적이지 않은 성격에서 명백하지만, 나중에 완전히 새로운 프로그래밍 언어로 발전했다.
- Java와 JVM(Java Virtual Machine)은 기업 공간에서 널리 사용되고 구현되어 왔으며, 이를 통해 여러 운영 체제에서 Java의 컴파일된 바이트코드를 실행할 수 있습니다. 성능이 중요할 때 일반적으로 좋은 작업용 언어입니다.
- C#은 Microsoft에서 .NET 이니셔티브의 일부로 설계했으며 CLR(공용 언어 런타임)이라는 가상 머신을 사용합니다. C#은 Java보다 운영 체제에서 덜 추상화되어 있으므로 C++ 코드를 C#과 혼합하여 사용할 수 있습니다.
- Client-side JavaScript (React): 브라우저에서 커피를 실행해야 할 때 선택은 단 하나뿐입니다. 바로 JavaScript입니다. 전체 페이지를 새로 고치거나 사용자 경험을 방해하지 않고 동적 사용자 인터페이스를 달성하려면 클라이언트 측 JavaScript가 메모리의 많은 상태를 관리해야 합니다.

[목차로 돌아가기](#midterm-guide--중간고사-가이드)

---

## 코딩

### 1. Node.js의 이해 / 시작하기

- Node: Node.js는 자바스크립트를 사용해 웹 서버를 만들 수 있게 해주는 런타임이다.
- npm commands: (init, install, --save-dev)
- package.json is a file that contains information about the project and the dependencies that are required to run the project. / package.json은 프로젝트에 대한 정보와 프로젝트를 실행하는 데 필요한 종속성에 대한 정보를 포함하는 파일입니다.
- package-lock.json is automatically generated for any operations where npm modifies either the node_modules tree, or package.json. / package-lock.json은 npm이 node_modules 트리 또는 package.json을 수정하는 모든 작업에 대해 자동으로 생성됩니다.
- node_modules is a directory that contains all the dependencies for the project. / node_modules는 프로젝트의 모든 종속성을 포함하는 디렉터리입니다.
- app = http.createServer();
- app.on("request", (req, res) => { ... }
- app.listen(port);

[목차로 돌아가기](#midterm-guide--중간고사-가이드)

---

### 2. 첫 번째 Node.js 웹 서버 만들기

- main.js
- router.js
- content-types.js
- utils.js
- public/ css/ js/ img/
- views/

[목차로 돌아가기](#midterm-guide--중간고사-가이드)
