

### Software Multi Tenancy 와 Cloud 에서의 Multi Tenancy

멀티 테넌시(Multi Tenancy) : 다중 소유 라는 뜻으로, 자주 언급되는 단어임에도 생각보다 정리가 잘 되어있는 곳이 별로 없어서 정리해보았다.

`소프트웨어 멀티 테넌시란 소프트웨어 아키텍처의 한 종류로 하나의 Software Instance 가 하나의 서버 위에서 여러 개의 Tenant 를 서비스 한다는 의미이다.`

여기서 `테넌트란 소프트웨어 인스턴스에 대해 공통이 되는 특정 접근 권한을 공유하는 사용자들을 말한다.` 

멀티 테넌트 구조에서 Software 들은 모든 테넌트들에 대해 인스턴스의 일부분을 단독적으로 제공하기 위하여 설계되어 있다.

이는 개개의 소프트웨어 들이 각기 다른 테넌트들을 위해 서비스되는 멀티 인스턴스 구조와 상반된다.

멀티 테넌시 환경에서 복수의 고객들은 동일한 데이터 스토리지 매커니즘과 함께 동일한 하드웨어의 동일한 OS에서 실행되는 동일한 Application 을 공유한다.

이는 구성 요소가 이양됨으로써 각 고객이 별도의 VM에서 구동되는 것처럼 보이게 하는 가상화와의 차이점이다.

`Multi Tenancy 란 하나의 소프트웨어를 여러 사용자가 함께 사용하는 것을 말한다.`

사용자들은 프로그램을 수정하는 것이 아니라 서비스 제공자가 제공하는 설정 기능을 통해 자신에 맞게 커스터마이징해서 이용한다.

하나의 시스템으로 여러 고객이 사용하는데 고객마다 관리할 필요가 없기 때문에 관리비용도 적게 들고 유지보수가 간편하다. 하지만 하나의 DB로 관리한다는 것은 그만큼 위험도가 높다는 뜻이다.

클라우드 컴퓨팅의 기본이 아키텍쳐를 공유하는 멀티 테넌시 시트템이다 라는 의견이 있으나 보안 문제가 우려가 되기 때문에 강력한 데이터 암호화 같은 기술이 병행되어야 한다.

많은 경우에 멀티 테넌시 시스템의 예시는 SaaS 의 형태라고 생각하면 된다. 

설명이 매우 추상적이라서 보충하자면 `일반적인 멀티 테넌시란 하나의 소프트웨어 인스턴스로 여러 고객에게 서비스를 제공하기 위한 아키텍쳐 그 자체를 말한다.`

이 개념이 클라우드 컴퓨팅에 적용되면서 제공하는 서비스가 가상머신이라면, 서비스 Provider 는 하나의 컴퓨터에 여러 개의 독립된 가상 머신을 만들어 다수의 테넌트에게 이 컴퓨팅 리소스를 서비스 할 수 있게 된다. 그리고 이게 클라우드 서비스 개념의 출발이다.

클라우드에서 공유 인프라 구축은 까다로운 문제이다.

전통적인 데이터센터 구조는 실 사용량에 비해 과도한 인프라가 구축되어 있어 리소스 활용률이 낮으며 이 때문에 클라우드 컴퓨팅을 통해 개별 어플리케이션, 그룹 또는 고객 간의 리소스가 공유되는 Multi tenant 환경을 이해하는 것이 중요하다.

많은 기업들(Client)이 보안과 QoS(Quality Of Service) 를 염려하여 클라우드 인프라 구축 및 서비스에 대한 계약을 망설이고 있다. 이러한 이유로 개발된 Secure Multi tenant architecture의 멀티 테넌시의 4대 요소는 다음과 같다.

1. 가용성 : 공유 인프라 한대에 장애가 발생하는 경우 다른 클라이언트에 영향을 줄 수 있기 때문에 장애가 발생할 수 있는 상황에서도 필요한 컴퓨팅, 네트워크 및 스토리지 리소스를 이용할 수 있도록 이중화 및 기타 메커니즘을 제공한다.
2. 안전한 분리 : 한 테넌트는 어떤 상황에서도 다른 테넌트의 VM, 네트워크 또는 스토리지 리소스에 접근할 수 없어야 한다. 각 테넌트는 안전하게 분리되어 있어야 한다.
3. 서비스 보장 : 정상적으로 운영되는 동안이나 장애가 발생했을 때나 특정 테넌트에서 비정상적인 부하가 발생했을 때에도 컴퓨팅, 네트워크, 스토리지가 분리되어 성능이 보장되어야 한다.
4. 관리 : 모든 리소스를 빠르게 프로비저닝, 관리 및 모니터링할 수 있는 기능이 매우 중요하다. 관리를 단순화 함과 동시에 고객이 특정 벤더에 얽매이지 않도록 하는 것이 중요하다. 타사 어플리케이션 벤더 도 전체 환경에 대한 관리를 제공할 수 있도록 모든 단계에서 API 통합 지점과 Work flow를 상세히 기술하는 것이 중요하다.

Public Cloud에서 대부분의 서비스 제공자(Provider)들은 Multi tenant 모델을 사용한다. 하나의 서버 인스턴스의 사용을 제공하고 유지보수 및 배포가 용이하며 비용면에서 효율적이다.

이 때 public cloud provider는 당연히 각 Client에게 Hypervisor 레벨로의 접근을 허용하지 않으며 당연히 host-level 의 utility 들(예를 들어 안티바이러스 등의 보안 프로그램들 또는 백업 프로그램들)의 설치 및 사용이 허용되지 않는다.

이러한 특성은 보안상의 영향 뿐 아니라 잠재적인 WAN / Cloud 에서의 Failure 을 포함한다.

또한 Public Cloud Provider 들은 그들의 하드웨어를 소유하고 Software들을 제어할 수 있기 때문에 Tenant 들의 동의를 구하지 않고도 저수준의 업데이트를 하는 것이 가능하다.

일반적으로는 OS 에 대한 업그레이드 이전에 광범위한 테스트가 수반되나 이런 종류의 업데이트가 Client 들의 소프트웨어에 영향이 미치지 않는다고 장담할 수 없다.

퍼블릭 클라우드 사용시 비용은 예측할 수 없는 경우가 많다. CPU, 메모리, I/O, 네트워크 리소스 등과 같은 경우 너무나도 많은 변수가 존재하며 이를 대응하기 위해서 효율적인 모니터링 툴이 필요하다.



---


### 싱글테넌트

![image](https://user-images.githubusercontent.com/62640332/156858385-dba3b358-cec5-4be6-8f0b-55708f79ead1.png)


그림에 표시된 두 기업 고객은 각각 별도의 물리 서버에서 개별적인 애플리케이션 인스턴스를 실행한다. 

2대의 서버는 동일한 데이터센터에 위치할 수 있고 같은 네트워크 인프라를 공유할 수도 있지만, 그 외의 다른 물리적 자원은 공유하지 않는다. 

기업은 별도의 CPU와 메모리, 스토리지 하드웨어로 개별적인 컴퓨터 인스턴스를 실행하기 때문에 왼쪽 및 오른쪽 기업의 정보가 상호 간섭을 일으키는 것은 쉽지 않으며, 사실상 불가능하다.

하지만 이 구성에 3번째 기업을 추가하려면 애플리케이션의 3번째 인스턴스가 필요하며, 이를 위해서는 3번째 물리 서버를 구매해야 한다. 

서버 하드웨어를 적절히 설정하고 소프트웨어를 설치하고, 업데이트를 하고, 구성도 해야 한다. 

일반적으로 기업 고객을 새로 추가하는 작업은 느리고 번거로우며, 비용도 많이 든다. 각 기업이 물리적 하드웨어 벽으로 구분된다는 것이 장점이다.

이것이 바로 싱글 테넌트(Single Tenant) 애플리케이션 모델이다.


### 멀티테넌트 가상화

![image](https://user-images.githubusercontent.com/62640332/156858414-4d692b72-038d-4d22-a3b5-af868890f97d.png)

<그림 2> 모델은 싱글 테넌트 모델처럼 두 기업이 애플리케이션의 2대의 개별 인스턴스를 사용한다. 다만, 이번에는 동일한 물리 서버에 존재하는 별도의 가상 서버 2대를 실행한다. 

이는 80년대 후반, 90년대 초반 이후 사용된 서버 가상화를 활용한 멀티테넌트의 한 예다. 

각 애플리케이션은 별도의 ‘논리적’ 서버에 있지만, 2대의 가상 서버는 동일한 물리적 하드웨어에 존재한다는 개념이다.

이 모델은 싱글 테넌트 모델에 비해 애플리케이션을 이식하고 소프트웨어를 이동하기가 더 쉽다. 

새 기업 고객을 추가하기 위해 적절한 하드웨어와 소프트웨어를 갖춘 새 물리 서버를 마련할 필요가 없다. 가상 서버의 새 인스턴스를 실행하기만 하면 된다. 

이 작업은 간단한 명령이나 API 호출로 가능하며, 일반적으로 쉽다. 물리 서버에 충분한 용량이 있는 한, API 호출로 여러 대의 가상 서버를 실행할 수 있다.

새 하드웨어는 부가적인 물리적 자원이 필요한 경우에만 필요하다.

사실 이 모델은 매우 강력해서 클라우드 컴퓨팅 시작의 발판이 됐다. 

클라우드 서비스 업체는 서버 가상화를 통해 기업을 대상으로 가상 서버 인스턴스를 직접 판매하고 수요에 따라 가상 서버 인스턴스를 시작 및 중지할 수 있다. 

이는 AWS EC2의 기초가 됐으며, 이후 마이크로소프트 애저, 구글 클라우드 플랫폼 및 기타 퍼블릭 클라우드에도 적용됐다. 

새 인스턴스는 일정 기간 동안 고객에 임대하고, 풀리면 다른 기업에 적용할 수 있다.

기업 고객은 가상 하드웨어 벽에 의해 서로 분리된다. 하드웨어 벽처럼 보이지만 가상 소프트웨어에 의해 시뮬레이션된다. 

또한, 기업을 추가하는 일은 쉽지만 여전히 새 가상 서버 인스턴스를 실행하는 과정이 필요하고, 여기에 자원이 소비된다.

이 모델을 물리적 멀티테넌트, 가상 싱글테넌트 모델이라고 한다.

이런 명칭은 가상 인스턴스가 기업의 자체 소프트웨어 인스턴스와 함께 단일 기업에 할당되지만(가상 싱글테넌트), 이 가상 인스턴스는 모두 공유되는 물리적 하드웨어에서 실행된다는 것에서 비롯됐다.

### 멀티테넌트 소프트웨어

![image](https://user-images.githubusercontent.com/62640332/156858503-ac806d2c-d3b3-4376-b7ad-e5c568c5ed47.png)


이 모델에서는 여러 고객이 동일한 애플리케이션 인스턴스를 공유하며 모든 인스턴스는 동일한 물리 서버, 동일한 물리적 인프라에서 실행된다. 

이 경우, 소프트웨어는 기업을 상호 분리하며, 이 때 물리적인 분리는 없다. 기업은 오로지 소프트웨어에 의해서만 분리된다.

이 모델을 물리적 멀티테넌트, 가상 멀티테넌트 모델이라고 부른다. SaaS 모델로 더 잘 알려져 있다.

이 모델에서는 기업 고객을 추가하는 작업이 매우 쉽다. 가상 또는 물리적 하드웨어는 불필요하다. 

기반 하드웨어에 충분한 자원이 있는 한 데이터베이스를 업데이트하거나 구성 파일에 항목을 추가하는 작업 만으로 기업을 추가할 수 있다.

기업 추가는 쉽고 빠르며, 비용도 많이 들지 않는다.


### 멀티테넌트는 안전한가?

과연 싱글 테넌트가 멀티테넌트보다 조금이라도 더 안전할까? 이 질문은 흔하면서도 답하기 어렵다. 

두 모델 모두 안전할 수도, 그렇지 않을 수도 있다. 소프트웨어를 공격하려는 악의적 행위자 측면에서 보면, 두 모델의 안전 레벨은 동일하다. 

둘 다 악의적 행위자에 대응해 보안을 유지하기 위해 안전한 프로세스와 절차가 필요하다.

우발적으로 발생하는 보안 취약점 측면에서는 어떨까? 예를 들어, 한 기업의 데이터를 실수로 다른 기업에 노출하는 경우가 있을 것이다. 

잘못 설계된 멀티테넌트 SaaS 애플리케이션은 분명히 한 기업의 데이터를 공유 환경을 이용하는 다른 기업에 노출할 위험이 있다.

![image](https://user-images.githubusercontent.com/62640332/156858617-057542cd-ef94-4e2d-b6b0-7c62ffaf4fb2.png)

먼저 <그림 4>의 왼쪽 위에 있는 오리지널 싱글 테넌트 애플리케이션부터 살펴보자. 

한 기업의 데이터가 다른 기업에 뜻하지 않게 노출되려면 데이터가 물리 서버 사이를 이동해야 하는데, 이는 쉽지 않은 일이다. 

이런 일이 우연히 발생하는 경우는 좀처럼 없을 것이다. 싱글 테넌트 시스템에서는 우발적인 보안 문제가 발생할 가능성이 상대적으로 낮다.

이제 <그림 4>의 오른쪽 상단에 있는 가상 서버 멀티테넌트 애플리케이션을 보자. 이 모델에서 데이터가 우발적으로 노출되기 위해서는 데이터가 강력한 가상 경계를 넘어 이동해야 한다. 

이런 일이 발생하는 경우는 상상하기 어렵지만 불가능한 일은 아니다. 

실제로 몇 년 전, 멜트다운(Meltdown)과 스펙터(Spectre) 취약점으로 인해 이런 유형의 노출을 유발할 수 있는 서버 가상화의 결함이 드러나기도 했지만 신속하게 발견 및 수정됐다.

<그림 4>의 하단에 위치한 오리지널 멀티테넌트 애플리케이션(SaaS 애플리케이션)에서는 소프트웨어 오류가 기업 간 상호 데이터를 노출시킬 여지가 더 크다. 

기업을 분리하는 벽이 전적으로 애플리케이션 계층에만 존재하고 기반 하드웨어 또는 가상화 수준에서의 분리는 없기 때문이다. 

이론적으로는 소프트웨어 버그로 인해 다른 기업의 데이터가 예기치 않게 노출될 수 있다.

이는 기업이 감수해야 할 위험이다. 하지만 실제로 평판 좋은 서비스 업체의 고품질 SaaS 애플리케이션을 사용하는 경우, 이 위험은 생각보다 크지 않다. 

테넌트 간의 의도치 않은 데이터 노출을 유발하는 취약점은 매우 신속하게 수정된다. 업체는 이 문제에 대해 각별한 주의를 기울인다. 

어쨌든 기업이 SaaS 기업을 선택하고 그 기업에 맡길 데이터를 결정할 때 고려해야 할 위험 요소다.

### 멀티테넌트를 사용해야 하는 이유

싱글 테넌트가 이론적으로 멀티테넌트보다 더 안전하다면, 멀티테넌트를 사용할 이유가 있을까?

먼저 앞서 언급한 사례에서 추론할 수 있는 것처럼, 멀티테넌트 시스템은 `확장과 신규 고객 추가가 더 쉽다.` 

`싱글 테넌트 시스템`에서 신규 고객을 추가하기 위한 `증분 비용은 매우 높다.` 새 하드웨어, 설치, 구성, 유지보수, 소프트웨어, 업그레이드 등을 위한 비용이 포함되기 때문이다. 

반면, 원래의 멀티테넌트 SaaS 시스템에서 신규 고객을 위한 증분 비용은 0에 가깝다. 데이터베이스에 말 그대로 줄 하나 추가하는 것으로 가능하기 때문이다. 

멀티테넌트 SaaS 시스템을 도입하면 서비스 업체는 애플리케이션에 ‘구매 전 체험하기’ 기능을 구축하고 수익성을 유지하면서 무료 티어를 구현할 수 있다.

또한, 멀티테넌트 시스템은 실행 중인 애플리케이션이 `부가적인 부하를 처리해야 할 때 훨씬 더 쉽게 자원을 추가`할 수 있도록 한다. 

부하를 처리하기 위해 특정 수만큼의 서버가 필요한 애플리케이션에서 트래픽이 급증하면 어떻게 해야 할까? 

가상 멀티테넌트 하드웨어가 있는 시스템에서는 즉석에서, 몇 초 만에 `손쉽게 서버 용량을 더 추가`할 수 있다. 

싱글 테넌트 애플리케이션이라면 물리적 서버를 구매, 설치, 구성하는 데 며칠 혹은 몇 주 걸릴 것이다.

싱글 테넌트 애플리케이션에서는 용량을 늘리는 데 너무 오랜 시간이 걸리기 때문에 몇 개월 전에 미리 용량을 계획해야 한다. 

앞으로 용량이 얼만큼 필요할지 예측하고, 예상치 못한 급격한 사용량 증대에 대비해 충분한 여분을 확보함으로써 ‘아무것도 하지 않은 상태’로 둬야한다. 

이 과잉 용량은 장기간 유휴 상태로 방치돼 애플리케이션 운영 비용을 증가시키는 요인이 된다.

멀티테넌트 시스템에서는 필요할 때 즉석에서 용량을 추가할 수 있다. 더 많은 가상 서버를 가동하기만 하면 된다. 

멀티테넌트 인프라의 하드웨어는 공유되기 때문에 과잉 용량이 발생해도 여러 기업 간에 분산돼 활용된다.

---

- 단일-테넌트: 각 데이터베이스는 한 테넌트의 데이터만을 저장합니다.
- 다중 테넌트: 각 데이터베이스는 (데이터 개인 정보를 보호하는 메커니즘을 사용하여) 별도 다중 테넌트의 데이터를 저장합니다.
- 하이브리드 테넌트 모델도 사용할 수 있습니다.

---



![image](https://user-images.githubusercontent.com/62640332/156861973-cd48d091-7068-469f-96b4-2747fc5b1061.png)


ㅁ Catalog based tenacy

![image](https://user-images.githubusercontent.com/62640332/156862000-a091272f-671f-40b4-8817-18fca9e92feb.png)


ㅁ schema based tenacy

![image](https://user-images.githubusercontent.com/62640332/156862032-b6d509a4-2c3f-4cd8-9a7d-37278eb77197.png)


ㅁ Table based multitenancy

![image](https://user-images.githubusercontent.com/62640332/156862068-4b020646-9357-48b0-8697-ea1fdfc49a53.png)


<br>
<br>

출처] 

https://jins-dev.tistory.com/entry/Software-Multi-Tenancy-%EC%99%80-Cloud-%EC%97%90%EC%84%9C%EC%9D%98-Multi-Tenancy

https://www.itworld.co.kr/news/216079
    
[azure muliti tenancy doc] https://docs.microsoft.com/ko-kr/azure/azure-sql/database/saas-tenancy-app-design-patterns

[aws muliti tenancy doc] https://docs.aws.amazon.com/ko_kr/cognito/latest/developerguide/cognito-dg.pdf#bp_user-pool-based-multi-tenancy   