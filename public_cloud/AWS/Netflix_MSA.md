


1. "넷플릭스 당하다"
 
"넷플릭스 당하다(Netflixed)"라는 말을 들어 보셨나요?    
이는 실리콘밸리에서 기존 비즈니스 모델이 붕괴하였을 때 사용하는 표현입니다.

실제로 넷플릭스는 지난 20년간 대형 DVD 대여점과 케이블 TV 등 미디어 업계의 골리앗들을 차례대로 쓰러뜨렸습니다.

동영상 스트리밍 서비스를 통해 전 세계적으로 1억 8천만 명이 넘는 가입자를 확보한 넷플릭스는 Netflixing(넷플릭스 본다), Netflix and chill(넷플릭스 보고 갈래?) 등의 신조어가 생길 만큼 높은 인기를 구가하고 있습니다.

넷플릭스는 어떻게 전 세계 사용자에게 고화질 동영상 서비스를 안정적으로 제공할 수 있을까요? 그 비밀은 운영시스템에 MSA(Microservices Architecture)를 도입한 것과 그것을 가능하게 한 넷플릭스 OSS(Open Source Software)에 있습니다.

2007년 심각한 데이터베이스 손상으로 3일간 서비스 장애를 겪은 넷플릭스는 신뢰성 높고 수평 확장이 가능한 클라우드 시스템으로 이전할 필요성을 느꼈습니다. 

단순히 플랫폼 이전만으로는 기존의 문제점과 한계를 탈피할 수 없다고 판단한 넷플릭스는 고가용성, 유연한 스케일링, 빠르고 쉬운 배포를 위해 MSA를 선택했습니다. 

그리고 MSA 전환을 위한 기술들을 도입하여 무려 7년에 걸쳐 클라우드 환경으로 이전하였습니다. 

이 과정에서 넷플릭스가 경험한 노하우와 문제해결 방법을 공유하기 위해 MSA 전환 기술을 오픈소스로 공개했습니다. 

이렇게 탄생한 넷플릭스 OSS는 MSA를 도입하려는 많은 사람에게 좋은 선택지가 되고 있습니다.

<br>
<br>

2. 넷플릭스는 MSA를 도입하면서 어떠한 고민을 했을까요?  

MSA에서 중요한 요소 중 하나는 자동 확장(Auto Scale-out)입니다.

 자동 확장이란 특정 서비스에 트래픽이나 부하가 증가할 경우 인스턴스를 추가로 생성하고, 반대로 트래픽과 부하가 감소할 경우 불필요한 인스턴스를 서비스에서 제거하는 것을 의미합니다. 
 
 서비스 단위로 자동 확장이 가능해 시스템 자원 활용을 최적화할 수 있지만 구현하기 위해서는 고려해야 할 것들이 많습니다. 
 
 예를 들어, 동적으로 추가하는 인스턴스 정보를 다른 서비스로 전달할 방법이 필요합니다. 
 
 또한 신규 추가된 인스턴스 간의 로드 밸런싱을 처리해야 하고 장애대응 방법도 마련해야 합니다. 
 
 게다가 서비스의 확장과 축소가 빈번하고 서버들의 물리적 환경이 다르다면 고민은 더 커질 것입니다. 
 
 넷플릭스는 이러한 난관을 어떻게 해결했는지 알아보겠습니다.

<br>
<br>

#### Spring Cloud Netflix

먼저 클라우드 환경에 특화된 프레임워크인 Spring Cloud를 살펴볼 필요가 있습니다. 

Spring Cloud는 Spring boot를 기반으로 MSA 구축에 특화된 라이브러리들의 집합입니다. Spring Cloud에는 Eureka, Hystrix, Ribbon, Zuul 등 많은 넷플릭스 OSS가 통합되어 있습니다. 우리가 알아볼 내용은 넷플릭스 오픈소스 중에서도 Spring Cloud에 속해 있는 Spring Cloud Netflix입니다.

클라우드 환경에 특화된 프레임워크인 Spring Cloud 그림입니다. Spring Cloud는 Spring boot를 기반으로 MSA 구축에 특화된 라이브러리들의 집합입니다. Spring Cloud에는 Eureka, Hystrix, Ribbon, Zuul 등 많은 넷플릭스 OSS가 통합되어 있는것을 볼 수 있습니다.
[그림 1] 넷플릭스 OSS와 Spring Cloud 관계

![image](https://user-images.githubusercontent.com/62640332/156034884-67133859-58ea-4e38-8f9d-c7417576f283.png)

<br>
<br>

#### 서비스 디스커버리 서버(Service Discovery Server) - Eureka

MSA 구조에서 서비스들은 동적으로 확장되고 축소되기도 하는데 이때마다 운영자가 일일이 인스턴스 정보를 수정, 관리하기란 쉬운 일이 아닙니다. 

따라서 인스턴스의 상태를 동적으로 관리하는 서버가 필요해졌는데 이를 보통 서비스 디스커버리 서버로 칭하며 넷플릭스는 Eureka라는 이름으로 공개하였습니다.



![image](https://user-images.githubusercontent.com/62640332/156034937-cb200536-a379-48e7-ad78-592b5266f9dd.png)

새로운 인스턴스는 시작할 때 Eureka 서버에 IP, 호스트 주소, 포트 정보 등을 스스로 전송합니다. 

Eureka 서버는 받은 정보를 가지고 일정한 간격으로 상태를 체크하면서 해당 인스턴스를 관리합니다. 

인스턴스가 새로 실행될 때마다 자신의 정보를 서버에 동적으로 등록하기 때문에 운영자들은 서비스를 수평 확장할 때 IP 정보에 대해 신경 쓸 필요가 없어졌습니다. 

(여기서 수평 확장이란 부하가 걸린 서비스에 인스턴스를 늘려 처리량을 높이는 것을 의미합니다.) 

운영자들은 설정 파일에 Eureka 서버 정보만 입력하면 되고, 서비스들은 다른 서비스를 호출할 때 Eureka 서버에 등록된 인스턴스를 조회하면 됩니다.

#### 클라이언트 사이드 로드 밸런서(Client Side Load Balancer) - Ribbon

모놀리식 시스템에서는 부하 분산을 위해 L4 스위치 같은 하드웨어 장비를 앞단에 두고 트래픽을 여러 서버로 분산하였습니다. 

이렇게 중앙 집중화된 방식은 로드 밸런서에 장애가 발생하면 전체 서비스에 문제가 생기는 위험을 동반합니다. 

또한 동적으로 서버가 추가, 삭제되는 환경에서 하드웨어 장비로 대응하는 것도 한계가 있습니다. 

넷플릭스는 소프트웨어로 구현한 클라이언트 로드 밸런서인 Ribbon을 추가했습니다. 

여기서 클라이언트의 의미는 PC나 모바일 단말기가 아닌 MSA에서 다른 서비스를 호출하는 클라이언트 서비스를 뜻합니다. 

클라이언트 서비스는 부하 분산 알고리즘에 따라 서버 목록 중 하나를 선택하여 호출합니다. 

이때 서버 목록은 정적 리스트를 사용하면 되지만 앞에서 설명한 Eureka와 연동할 경우에는 동적 리스트도 가능합니다.



![image](https://user-images.githubusercontent.com/62640332/156034992-73f8271c-d67a-41ae-aef1-a91c5ed4cf89.png)

사용할 수 있는 알고리즘으로는 순서대로 선택하는 Simple round robin, 서버의 응답 시간에 따라 선택하는 Weighted response time, 3회 연속 호출 실패 시 30초 동안 목록에서 제외하는 Availability filtering 등이 있습니다. 

이 외에도 Zone-aware round robin, Random load balancing 등 다양한 알고리즘이 있으므로 상황에 따라 적절한 로드 밸런싱 전략을 선택하면 됩니다.

<br>
<br>

#### 서킷 브레이커(Circuit Breaker) - Hystrix

MSA도 특정 서비스에 과부하가 걸리거나 어떤 문제로 인해 정상적으로 작동하지 않으면 전체 서비스에 장애를 전파하는 경우가 있습니다. 

특정 서비스에 문제가 생기더라도 전체적으로 장애가 확산하지 않도록 차단해주는 기능을 서킷 `브레이커`라고 하며 넷플릭스는 이를 Hystrix라는 이름으로 개발하였습니다. 

Hystrix 서버는 각 서비스의 오류 상태나 복구 상태 그리고 현재 오류 내용이 무엇인지를 파악합니다. 

API 호출 통계를 기반으로 상대 서비스에서 이상을 감지하면 즉시 통신을 중단합니다. 

그러면 문제가 있던 서비스를 격리(Isolation)하게 되는데 이후에는 문제가 해결될 때까지 별도의 스레드에서 밀린 작업을 수행하거나 호출 수를 제한합니다.

상태가 정상으로 돌아오면 통신을 연결하여 다시 호출을 받도록 합니다.

서킷 브레이커의 또 다른 중요한 기능은 `폴백(Fallback)`입니다. 

폴백은 정해진 시간 내에 호출이 실패하면 대신 동작하는 예외처리로 보면 됩니다. 

개발자가 폴백 메소드를 구현함으로써 시스템 장애로부터 유연하게 복구를 실행할 수 있습니다. 

또한 서킷 브레이커의 정보나 각 서버의 상태를 확인할 수 있는 모니터링 서비스까지 제공하여 로그를 중앙 집중형으로 관리하고 검색할 수 있습니다.


![image](https://user-images.githubusercontent.com/62640332/156035020-bf2c8789-feda-49c7-8b30-ef0f5bd6c998.png)


#### API 게이트웨이(Gateway) - Zuul

Zuul은 넷플릭스가 개발한 Spring Cloud Netflix에 특화된 API 게이트웨이입니다. 

API 게이트웨이는 사용자 요청을 적절한 서비스로 프록시 혹은 라우팅하는 MSA의 컴포넌트입니다. 

Zuul은 최전방에서 클라이언트의 요청을 받아 적절한 서비스에 전달하고 결과를 다시 클라이언트에 보내는 엣지 서버(Edge Server)로 보면 됩니다. 

그런데 사용자에게 Zuul만 노출하고 다른 마이크로서비스의 종단점(Edge)을 숨기는 이유는 무엇일까요?

MSA 환경은 하나의 서비스에 여러 개의 서버가 존재할 수 있기 때문에 사용자에게 다수의 진입점(End Point)이 생겨납니다. 

진입점은 인증과 보안, 잘못된 요청 등을 처리하는데 일부 진입점에 변경이 생길 경우 전체가 영향을 받기 때문에 관리가 까다롭습니다. 

이때 Zuul을 활용해 도메인을 하나로 통합하고 단일 진입점으로 사용한다면 관리가 수월해집니다.

또한 필터 기능을 제공합니다. 사용자가 많은 서비스에는 다양한 형태의 요청이 쏟아집니다. 

넷플릭스의 경우, 초당 수십만 개 이상의 요청이 들어오는데 수천 개가 넘는 장치 유형과 수백 개의 국가 유형별로 구분지어 처리해야 합니다. 

요청 중에는 예상치 못한 것도 있어 운영 이슈가 발생할 수 있습니다. 

Zuul 필터는 사용자 요청에 대해 각 리소스의 인증 요구사항을 식별하고 이를 만족시키지 않는 요청은 거부합니다. 

필터는 동적으로 작동하기 때문에 정책이 바뀌어도 별도의 배포없이 반영할 수 있습니다.

이 외에도 Zuul은 데이터 및 통계를 분석하여 모니터링이 가능합니다. 또한, 스트레스 테스트, 멀티 리전(Multi-region) 복원 등의 기능도 지원합니다.

![image](https://user-images.githubusercontent.com/62640332/156035063-2bcd233e-4aca-4932-833c-cd104aa67d2d.png)


<br>
<br>

3. Spring Cloud Netflix를 이용한 MSA 도입

넷플릭스는 2008년부터 2016년까지 이용자가 8배, 월간 시청 시간이 1천배 가량 증가했음에도 MSA 환경 구축을 통해 고객들에게 원활한 서비스를 제공할 수 있었습니다. 

MSA 방식을 도입한 다른 기업으로는 트위터, 페이스북, 이베이, 페이팔, 우버 및 나이키 등이 있습니다.

이들이 전적으로 Spring Cloud Netflix를 사용하는 것은 아니지만 MSA의 선두주자인 넷플릭스의 영향을 많이 받았고 그들의 오픈소스를 적극 활용하고 있는 것은 사실입니다.

해외뿐 아니라 국내에서도 많은 기업이 MSA를 도입했는데 대표적으로 11번가, 배달의민족, 쿠팡 등이 있습니다. 

이 중 가장 최근에 Spring Cloud Netflix를 활용하여 MSA 전환에 성공한 11번가의 개발자는 넷플릭스 오픈소스가 기능 하나하나에 많은 경험이 녹아 있어 높은 완성도를 보인다고 말했습니다. 

또한 기존에는 밤샘 배포, 잦은 장애, 너무나 커진 공통코드 등 개발 환경이 비효율적이었는데 MSA로 전환하면서 이러한 문제점들이 근본적으로 해결되었다고 밝혔습니다.

기존의 아키텍처를 버리고 MSA로 전환하는 것은 부담스럽고 어려운 일입니다. 

MSA를 고려하고 있다면 서비스 특성과 운영 환경이 MSA에 적합한지에 대한 검증이 선행되어야 합니다. 

MSA로의 전환이 적합하다면 보유 중인 핵심자원을 버리는 과감한 선택이 필요합니다. 

기술이 빠르게 발전하는 현대 산업에서 핵심자원은 언제든지 바뀔 수 있기 때문입니다. 

이는 결코 쉬운 일이 아니지만, 우리에게는 앞서 다른 기업이 겪었던 어려움과 이를 극복한 결과물인 Spring Cloud Netflix가 있습니다.

 Spring Cloud Netflix를 명확하게 이해하고 서비스에 반영한다면 MSA로의 전환은 결코 어려운 일이 아닐 것입니다.


출처] https://www.samsungsds.com/kr/insights/msa_and_netflix.html