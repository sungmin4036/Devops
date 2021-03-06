ㅁ devops 5가지 철학

1. 문화(Culture) : DevOps를 통해 하나의 문화를 만들어 나갑니다.
2. 자동화(Authomation) : 자동화를 통해 효율성과 빠른 속도를 지향합니다.
3. 측정(Measurement) : 지표를 측정하여 지속적으로 개선해 나갑니다.
4. 공유(Shareing) : 공유를 통해 함꼐 발전해 나갑니다.
5. 축적(File up & Pile up) : 기록을 축적하여 자산을 만들어 나갑니다.

데브옵스는 어떤 요구사항을 효율적으로 만족시키기 위하여, 일을 자동화하며 변경사항 지표들을 측정, 공유하고 이 모든 결과물들을

지속적으로 축적해 나아가는 문화를 만들어가는 철학, 방법론, 기술


ㅁ Devops 업무

1. 서비스 개발과 배포를 신속하고 정확하게 만드는것
2. 서비스와 팀의 문제를 빠르고 정확하게 감지하는것
3. 장애 최대한 빠른시간안에 해결하는것
4. 확장가능하고 신뢰할만한 아키텍쳐를 만드는것
5. 데이터에 기반한 원활한 의사소통이 가능하게 하는 것

![image](https://user-images.githubusercontent.com/62640332/155358746-a97b04c9-1046-4463-93fd-444bc4763825.png)

![image](https://user-images.githubusercontent.com/62640332/155358947-f894a85a-cf56-4655-8a4b-5f95e07c956a.png)

빨간색을 원하지만 실제로는 힘들다.

전문인력의 부족과 의사소통 문제, 사람들간의 갈등 등 많이 발생한다.

서비스에따라 다 다르고, 문제가 수도없이 존재한다.

![image](https://user-images.githubusercontent.com/62640332/155359164-6786241e-a80e-4803-b660-408c3144a665.png)

특정시간에 백배이상의 트래픽이 발생한다.

분당 100만 트래픽을 해결해도 1000만 은 완전히 다른 문제다.

![image](https://user-images.githubusercontent.com/62640332/155359420-2e704ff3-a1a0-4401-8f35-8e356491f428.png)

ㅁ 중앙관리

- 중앙관리는 표준화가 용이하다. 인프라를 관리하는 팀이있기 떄문에 표준화를 하고, 모범사례를 구축하는데 유용하다. 
- 인프라팀(devops)은 규모가 어느정도 있어야하고, devops(전문인력)이 따로 필요로한다. 한번 잘못되면 계속 잘못될수있다. 

인프라 만들때 서비스의 성격 및 의사소통, 문서화가 필요해서 의사소통 고도화 필요

ㅁ 자체 솔루션

- 해당 플랫폼을 제작하기때문에 원하는 형태로 만들수 있지만, 모든걸 만들고 유지보수를 해야하기 때문에 힘들다. ==> 인력이 많이 필요하다.


ㅁ PaaS

- 서비스를 이용하는것으로 접근이 쉽고, 쓰기가 쉽다. 인프라의 수준있는 인력이 없을경우 사용이 좋다. 그러나 해동 서비스에 종속된다. 원하는 방식으로 만들기 힘들다.

플랫폼에 묶이게 되어 모범사례 구축이 힘들고, 서비스가 발전할수록 원하는 서비스 구축이 힘들다. 대부분 그래서 PaaS를 하다가 고도화 되면서 한계를 느끼게 된다.


<br>
<br>
<br>

![image](https://user-images.githubusercontent.com/62640332/155360244-36da779e-4c1f-4344-8e7d-307a17823bee.png)

aws에서 만든 첫번째로 만든 컨테이너와 서버리스를 위한 완전관리 서비스. 지금까지 오픈 및 상용서비스가 많았지만 AWS에서 처음으로 만듬.

Proton을 안쓰더라도 데브옵스에 대한 CI/CD 를 알수있다. 수많은 AWS를 겪은 경험을 통해 proton을 만들었기에 전체적인 흐름과 생각을 알수 있다.

인프라 관리자는 규칙을 만들고, 표준과 모범사례, 보안사항 등을 만들수 있다. 
개발자는 이것을 보고 적합한 애플맅케이션을 선택해서 배포를 한다. => 인프라 관리자가 만들어놋 템플릿을 선택해서 사용한다.

모범사례는 과정이 반드시 단계별로 존재하고 즉, 파이프라인(CI/CD) 화가 되야 한다. + 모니터링 + 코드로써 인프라 가 되야 한다.

![image](https://user-images.githubusercontent.com/62640332/155361234-bc30de9c-a9fa-43ab-9118-01f1ec48bfd5.png)

- proton의 핵심 기능

 1. Self-service 인프라 개발자를 위한 코드 기반의 배포
 2. 중앙관리의 이점 원클릭 업그레이드
 3. 외부 솔루션과 통합

- protoon의 기본 개념

: proton은 Environments와 service 로 이루어져 있다.

 1. proton의 환경은 실제 서비스가 위치하게 될 기본 공유자원을 정의합니다. 예를들어 VPC와 Cluster
 2. 서비스는 환경안에서  실제로 돌아가게될 컴퓨팅 자원을 이야기하빈다. 예를들면 AWS Fargate, AWS Lambda


![image](https://user-images.githubusercontent.com/62640332/155361971-75593cd5-2259-45fb-8c9d-d6f37ae27041.png)


마이크로서비스 기본 아키텍처 storefront 웹서비스, 에 inventory, checkout 서비스를 가지고있다.  좀더 큰 규모라면 큐, 캐시, dynamodb 사용을 추가하면 된다.


![image](https://user-images.githubusercontent.com/62640332/155362031-746c3734-7fd4-4f4c-88b0-32ae51f1d9b9.png)

인프라 관리자가 envirement와 service template를 정의하고 생성 한다. vpc나 cluster에 해당된다.

개발자는 이 템플릿을 원하는것을 원하는것만 선택해서 바로 사용하여 개발에만 집중할수 있는 환경을 만들어야한다.

![image](https://user-images.githubusercontent.com/62640332/155362333-da445217-39ae-47c7-a92e-f59dae312453.png)

모든 환경을 일치시켜 업무 포퍼먼스를 좋게 할수 있게 하기위해 다 일체화 한다.

문제 발생시 추적을 하게 된다. 개발자 코드 문제인지, 인프라 설정인지 보안사항인지 방화벽 문제인지 다양한 방면에서 고민해야한다.

모든 개발 환경을 모두 의도한대로 일치시킬수 있다면, 인프라에대한 설정은 제외할수 있게 된다. 개발자는 개발에 집중할수 있게 된다.

자기가 잘하는 업무에 대해서 집중할수 있기에 업무 포퍼먼스를 좋게 한다.

![image](https://user-images.githubusercontent.com/62640332/155362780-db0d3d26-5168-4ba0-a39b-384326431ffe.png)

동일한 템플릿으로 다양한 서비스를 만들기 가능하다. DNS를 만들때 서브 도메인만 지정하면, 서브 도메인에따라 개발환경, 스테이징환경, 프러덕션 환경인지를 결정하기도 하니까

이런식으로 다양한 환경을 만들기도 한다.

