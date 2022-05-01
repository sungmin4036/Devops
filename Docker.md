



![image](https://user-images.githubusercontent.com/62640332/166149576-e5067870-0438-46d4-90f2-b53b525c5914.png)

### ㅁ 도커란?

![image](https://user-images.githubusercontent.com/62640332/166149629-bbec30f9-8ace-476d-8add-0b99d67de282.png)

: 컨테이너 기반 가상화 도구

- 가상화의 등장배경
: 새로운 프로젝트를 구동하려고하니 이전 서비스와 연동이 안되는일 발생

-> 서버의 성능을 나눠서 사용하여 해결 => 가상화의 등장

하나의 서버 자원을 나눠 가지며, 성능을 분산시키고, 분산된 서버들은 각기 다른 서비스 수행 가능하게 됨.

가상화를 통해 사용자가 많은 서비스는 많은 자원 할당하고, 적게 사용하는것은 적게 할당 하게 됨.

1. 서버가상화 - 하이퍼 바이저
: 하나의 물리적 서버 호스트에서 여러 개의 서버 운영 체제를 게스트로 실행할 수 있게 해주는 소프트웨어 아키텍처 

하이퍼 바이저는 여러개의 운영체제를 하나의 호스트 os를 생성해서 사용할수 있게 해주는 소프트 웨어

이렇게 생성된 여러개의 운영체제는 가상머신이라는 단위로 구별된다.

하이퍼바이저에 의해 생성되고 관리되는 운영체제는 게스트운영체제(Guest OS) 라고하며, 

각 게스트 운영체제는 다른 게스트 운영체제와는 완전히 독립된 공간과 시스템 자원을 할당받아 사용한다.

하이퍼바이저는 OS들에게 자원을 나누어 주며 조율한다. OS의 커널을 번역해서 하드웨어에게 전달한다.

대표적인  가상화 툴 ex) 버츄얼 박스, vmware

각종 시스템 자원을 가상화하고 독립된 공간을 생성하는 작업은 반드시 하이퍼바이저를 거치기 때문에, 일반 호스트에 비해 성능 손실이 발생

또한 가상머신에는 '게스트 운영체제'를 사용하기 위한 라이브러리, 커널 등을 전부 포함하기 때문에 배포하기 위한 이미지로 만들었을때 크기 또한 커진다.

즉, 가상머신은 완벽한 OS를 생성할수 있지만 성능이 느리고, 용량상으로 크다.

작은 애플리케이션을 구동하는데 OS까지 새로 띄우는 것이 부담스러움 -> 컨테이너 등장


<br>
<br>

![image](https://user-images.githubusercontent.com/62640332/166149131-5025f387-8d6e-4b01-90a9-a7b704a0ce6e.png)




### - 컨테이너란?

: 가상화된 공간을 생성하기 위해  리눅스 자체 기능인 chroot, 네임스페이스, cgroup을 사용함으로써 프로세스 단위의 격리환경을 만든다.

도커 엔진위에 컨테이너 할당, 컨테이너안에는 애플리케이션을 구동하는데 필요한 라이브러리 및 실행 파일만 존재.

그렇기 떄문에 이미지 만들었을때 이미지의 용량 또한 가상머신 대비 대폭으로 줄어든다.

따라서 이미지를 만들어 배포하는 시간이 매우 빠르며, 가상화된 공간 사용시 성능 손실도 거의 없다.


<br>
<br>

### - 가상화 관점에서 컨테이너란?

: 이미지의 목적에 따라 생성되는 프로세스단위의 격리환경.

이미지는 간단히 컨테이너를 만들기 위한 틀

컨테이너는 환경을 제공하며 프로세스의 생명주기를 관리한다.


![image](https://user-images.githubusercontent.com/62640332/166149150-ca33b8a7-e1cf-4cb0-8cd6-f5e41444996f.png)

컨테이너 예시로, 컨테이너를 자세히 보니 springBoot 프로세스와 Nginx 프로세스가 각각 할당되어 격리되어있음.

mysql은 따로 설치했다고 가정하며, Docker engine 위에는 설치 안한걸로 가정

그림에서 확인할수 있듯이 컨테이너는 파일시스템과 격리된 시스템자원 및 네트워크를 사용할 수 있는 독립 공간을 가진다.

컨테이너가 실행되면, 프로세스 실행에 필요한 자원들을 할당받고 프로세스를 실행한다.

이떄 커널을 통해 필요한 자원을 가져온다.

프로세스는 OS 위에서 실행된다, 이것을 `Host OS`라 부름.

그렇다면 호스트 입장에서는 컨테이너를 어떻게 바라보는가?

앞에서 말했듯이 컨테이너는 프로세스를 관리하며 실행하는 하나의 프로세스라고 말할수 있다.

즉, SpringBoot 애플리케이션 프로세스를 직접 실행하나 컨테이너로 실행하나 호스트 입장에서는 같은 프로세스로 똑같이 본다.

<br>
<br>

### - 컨테이너를 왜 써야할까?

: 컨테이너는 프로세스를 격리된 환경에서 관리한다.

이때 격리된 환경은 Host OS와의 격리를 의미하며 이를 통해 컨테이너에 어떤 설정을 하든 HostOS에 영향을 끼치지 않는다.

즉, 우리만의 독립된 개발 환경을 보장 받기 가능하다.

이를 통해 프로세스를 컨테이너 단위로 바라볼 수 있게 되고 프로세스의 관리, 확장이 용이해진다.

<br>
<br>

### - 프로세스 엔진을 어떻게 관리할수 있는가?

: Docker Engine을 사용하여 관리할수있다.

도커 엔진이은 유저가 컨테이너를 쉽게 사용할 수 있게 해주는 주체 입니다.

컨테이너의 라이플 사이클을 관리하며, 컨테이너 생성하기 위한 이미지관리, 컨테이너의 데이터를 저장하기 위한 저장소 역할을 하는 볼륨의 관리

컨테이너의 접속을 하기위한 네트워크 관리 등의 기능을 제공한다.

![image](https://user-images.githubusercontent.com/62640332/166149382-a11278fc-4e8f-4ec1-b27f-7a7123cf5145.png)

Dockerd에 있는 8개의 사각형에 대해서 각각 `프로젝트`라고 부르며, 컨테이너를 어떻게 사용할것인가에 대한 목적에 따라 분리되어 있다.

<br>
<br>

### - 사용자가 도커 명령을 쳤을떄 어떤 플로우 진행 될것인가?

![image](https://user-images.githubusercontent.com/62640332/166149515-d21d090f-e147-4210-a3fe-63d7a30d9226.png)

1. 사용자가 docker 명령어로 도커 엔진에게 명령어를 보낸다.
2. 이를 전달받은 도커 클라이언트는 /var/run/docker.sock에 위치한 유닉스 소켓을 통해 도커 데몬의 API 를 호출한다.
3. 도커데몬은 명령어에 해당하는 작업을 수행하고, 수행결과를 도커 클라이언트에게 반환하며 사용자에게 결과를 출력한다.
4. dockerd는 컨테이너를 생성하고, 실행하며 이미지를 관리하는 주체이다. 도커 프로세스가 실행되어 입력을 받을 준비가된 상태를 `도커데몬` 이라고 부른다.

<br>
<br>

![image](https://user-images.githubusercontent.com/62640332/166149559-ef54a6c6-9c2b-4232-9363-d2d297c48fe1.png)

### - 도커 데몬에게 명령 직접 전달도 가능하다.

1. 이때는 url 요청을 보내 명령어를 쳤을때와 같은 동작을 수행 가능하다. 


---

위의 내용은 단일 서버에서의 단일 도커 엔진에 대한 내용. 

지금 부터의 내용은 여러 서버에서의 엔진에 대한 내용

---

![image](https://user-images.githubusercontent.com/62640332/166149688-69983b0a-aa70-414f-b8e1-b6d9725da8f5.png)

하나의 호스트 머신에서 컨테이너가 많아져 cpu, memory, disk 용량 같은 자원이 부족해지기 시작

새로운 컨테이너를 추가하려는데 자원부족으로,  추가하지 못하는 상황이 발생함

제일 간단한 방법은 좋은 성능의 서버를 구매하는것 `scale up` 이라고도 한다.

하지만 자원의 확장성 측면이나 비용측면에서 좋지 않은 해답이다.

자원이 부족할때마다 자원을 더 사야한다던가, 막상 구매하여도 전부 사용하지 않기 때문.

![image](https://user-images.githubusercontent.com/62640332/166149791-47367921-2f59-42c8-946b-116ae4534a7a.png)

여러가지 방법이 있지만, 가장많이 사용하는 방법은 여러대의 서버를 클러스터로 만들어 자원을 병렬로 확장하는것. `scale out`




예를들어 4GB의 메모리가 탑재된 서버 1대에 도커엔진에 설치해 실제 운영환경에 사용한다고 가정한다.

이 1대의 서버에 컨테이너가 너무 많이 생성돼 있어 더는 컨테이너를 사용할수 없다고 판단되면

4GB의 메모리가 탑재된 새로운 서버를 추가해 자원을 늘리는것이다. 그림에서는 2개의 Host Os가 하나의 클러스터 단위로 묶여있다.

![image](https://user-images.githubusercontent.com/62640332/166149886-55264b97-f27a-4411-bc5b-114fd0f8a75b.png)


```
클러스터란?

각기다른 서버들을 하나로 묶어 하나로 묶어서 하나의 시스템같이 동작하게 함으로써 클라이언트들에게 고가용성의 서비스를 제공하는것.
```

![image](https://user-images.githubusercontent.com/62640332/166149949-f9f7e2f8-996f-4bf5-bd2b-48a1353e4ecc.png)

동일한 network 풀을 쓰며 요청에 따라 트래픽을 분산시킬수 있다.

하지만 여러대의 서버를 하나의 자우너 풀로 만드는것은 어려운 일이다.

새로운 서버나 컨테이너가 추가시 이를 발견하는 작업부터, 어떤 서버에 어떤 컨테이너를 할당할 건지에 대한 작업들 등을 처리해야할 작업이 많다.

=> `도커 스웜`의 등장

스웜모드는 마이크로 서비스 아이켁처의 컨테이너를 다루기 위한 클러스터링 기능에 초점을 두고 있다.

같은 컨테이너를 동시에 여러개 생성해 필요에 따라 유동적으로 컨테이너 수를 조절할수 있다.

컨테이너로의 연결을 불산하는 로드밸런싱 기능을 자체적으로 지원해요.

scale out 기본적으로 지원하지만 자체적으로 인스턴스를 늘리거나 줄이거나는 할 수 없고, 직접 해야한다.

스웜은 도커 엔진 자체에 내장되어 있다.

![image](https://user-images.githubusercontent.com/62640332/166150082-d7e46431-80ce-4bbb-8769-cb1b7eae1b43.png)

도커 엔진 프로젝트 안에 Swarmkit 포함되어 있으며, 스웜 모드는 매니저 노드와 워커노드로 구성되어 있다.

![image](https://user-images.githubusercontent.com/62640332/166150189-f0aba4b6-7be5-437d-be3e-1723a866cd74.png)


- 워커 노드는 실제로 컨테이너가 생성되고 관리되는 도커 서버

<br>

- 매니저 노드는 워커 노드를 관리하기 위한 도커 서버, 매니저 노드는 기본적으로 워커 노드의 역할을 포함
- 매니저노드는 운영환경에서 다중화를 하는 것이 좋다. 매니저 노드의 부하를 분산하고,  특정 매니저 노드 다운시, 정상적으로 스웜 클러스터를 유지할수 있기 때문이다.



<br>
<br>

### - 클러스터 구축은 어떻게 이루어 지는가?

- AWS EC2 인스턴스의 예시

![image](https://user-images.githubusercontent.com/62640332/166150232-0e65e9b1-ab09-4ec9-9e33-b2f2d83bba39.png)

4개의 인스턴스가 준비되어있으며, 인스턴스 1은 매니저노드, 인스턴스 2,3,4 는 워커노드

노드를 지정했으면, 역할 지정을 해줘야 한다.

![image](https://user-images.githubusercontent.com/62640332/166150304-a9230c51-18f9-4c89-901a-3e75e547a937.png)

1. 도커 명령어인 docker swarm init을 통해 매니저 노드를 설정한다.
2. docerk swarm join을 통해 노드를 추가 한다. => 워코노드를 추가함으로써 하나의 클러스터 단위가 완성됨, 매니저 노드 1개도 클러스터라 말할수 있다.
3. 

일반적인 도커 명령어의 제어 단위는 `컨테이너`  이는 도커 클라이언트가 제어하는 것은 컨테이너라는것

도커 스웜에서의 제어 단위는 `서비스` 서비스는 같은 이미지에서 생성된 컨테이너 집합을 의미.

![image](https://user-images.githubusercontent.com/62640332/166150494-1d332ed3-23c7-4600-a2ae-ed17fd372f30.png)

서비스를 제어하면 해당 서비스 내의 컨테이너에 같은 명령이 수행된다.

이때 서비스 내의 컨테이너를 `Task` 라고 부른다.

서비스의 정의에 따라 Task를 할당할 적합한 노드를 선정하고, 선택된 노드에 테스크를 분산해서 할당한다.

함께 생성된 테스크를 `레플리카(replica)` 라고 하며, 서비스에 설정된 레플리카의 수만큼 테스크가 스웜 클러스터 내에 존재해야 한다.

그림에서는 아무 노드에, 레플리카셋을 3으로 두었습니다.


![image](https://user-images.githubusercontent.com/62640332/166150551-ba054ee3-6d58-47f5-86d9-35185d38709f.png)

추가적인 예시, Springboot, nginx 즉, 2개의 서비스를 정의

SpringBoot는 모든 노드에 생성될 테스크의 수를 3개로 설정했고, Nginx는 모든 노드에 2개로 설정

![image](https://user-images.githubusercontent.com/62640332/166150560-52c63986-3b61-4d05-ac2d-f93851fe0730.png)

만약 노드에 장애가 발생한다면 스웜은 서비스의 테스크들에 대한 상태를 계속 확인하다가 서비스 내에 정의된 레플리카 수만큼 스웜클러스터 내에 존재하지 않으면,

새로운 테스크 레플리카를 생성한다.

![image](https://user-images.githubusercontent.com/62640332/166150601-5d5dfafd-8c39-40cb-96ea-357f7e2a98c0.png)

즉 그림과 같이 하나의 노드가 다운되면, 다른 노드에 테스크를 생성한다.

하지만 매니저노드가 다운돼버리면 클러스터가 사라진다. 이밖에도 스웜 모드가 제공하는 기능들은 많다.

- 클러스터 관리
- 서비스 관리
- 클러스터의 네트워크를 관리
- 클러스터 내의 노드를 관리하는 기능

### - 스웜모드를 왜 써야 할까?

: 서비스의 확장/관리를 편하게 하기 위해

### - 컨테이너를 어떻게 효율적으로 생성할수 있을까?

: 각각의 서비스가 동작하기 위해선 컨테이너가 필요, 서비스에 필요한 컨테이너가 1 ~ 2개 정도라면 도커 명령어를 직접 입력해 생성할 수 있지만

서비스가 여러개라면 말이 달라집니다.

하나의 프로젝트 단위를 클러스터 내에 묶었고 프로젝트가 구동되기 위해서는 SpringBoot, Nginx 컨테이너가 필요하다.

이 컨테이너들을 기반으로 테스크가 생성되기 때문이다.

매번 명령어를 통해 서비스에 필요한 컨테이너를 생성할수도 있지만, 이는 비효율적이다.

이에 대한 해답으로 `도커 컴포즈`를 사용한다.

### - 컴포즈란?

![image](https://user-images.githubusercontent.com/62640332/166150787-90d66b03-bc95-40e1-93bf-f5b03efaa863.png)

: 여러개의 컨테이너를 하나의 서비스로 정의하고 실행한다. 스웜 모드의 서비스와 유사하게 설정파일에 정의도니 서비스의 컨테이너 수를 유동적으로 조절 가능.

서비스 디스커버리도 자동으로 이루어짐.

컴포즈는 도커 엔진 밖에 위치한다. 그렇기 때문에 컴포즈를 직접 설치가 필요하다.

![image](https://user-images.githubusercontent.com/62640332/166150860-08758516-cb25-4c01-9cad-a74855ca0da7.png)

![image](https://user-images.githubusercontent.com/62640332/166150829-3baa4151-b3f4-4455-9aee-e1474414c7a0.png)

1. 도커 컴포즈는 컨테이너에 설정이 정의된 yml 파일을 읽어 도커 엔진을 통해 컨테이너를 생선한다.
2. 미리 yml 파일을 만들고, 위 예시는 nginx 와 springboot 서비스를 정의했다.
3. 파일 작성후 docker-compose 명령어를 통해 컨테이너 생성

### - 도커 컴포즈 구조

![image](https://user-images.githubusercontent.com/62640332/166150877-61f14938-bf34-4e09-ab11-b2e0c9d42747.png)

: 도커 컴포즈는 기본적으로 docker-compose.yml이 위치한 디렉터리 이름을 프로젝트 이름으로 사용한다.

즉, yml 파일이 저장된 디렉터리 이름에 따라 프로젝트의 이름이 달라진다. 물론 직접 설정 가능

하나의 프로젝트는 여러개의 서비스로 이루어지고 하나의 서비스에는 여러개의 컨테이너가 존재할수 있다.

이 컨테이너 안에 4개가 보이는데 각 컨테이너는 번호를 붙여 서비스 내의 컨테이너를 구별한다.

### - 컴포즈를 왜 사용해야 할까?

컨테이너의 생성을 편리하게 하기 위해 

\# 쿠버네티스는 지금까지 나온 기능들을 쉽게 사용하기 위해 나온것
