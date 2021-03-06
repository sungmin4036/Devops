### GitOps란?

GitOps는 DevOps의 실천 방법 중 하나로 애플리케이션의 배포와 운영에 관련된 모든 요소들을 Git에서 관리(Operation) 한다는 뜻입니다

![image](https://user-images.githubusercontent.com/62640332/156988420-fc1a4e14-c726-4423-a86e-eb8a27201363.png)

아주 간단하게 말해서 GitOps는 Kubernetes Manifest파일을 Git에서 관리하고, 배포할때에도 Git에 저장된 Manifest로 클러스터에 배포하는 일련의 과정들을 의미합니다.

#### GitOps의 원칙Permalink

1. 모든 시스템은 선언적으로 선언되어야 함
“선언적(declarative)”이라 함은 명령들의 집합이 아니라 사실(fact)들의 집합으로 구성이 되었음을 보장한다는 의미입니다.
쿠버네티스의 manifest들은 모두 선언적으로 작성되었고 이를 Git으로 관리한다면 versioning과 같은 Git의 장점과 더불어, SSOT(single source of truth)를 소유하게 됩니다.

2. 시스템의 상태는 Git의 버전을 따라감
Git에 저장된 쿠버네티스 manifest를 기준으로 시스템에 배포되기 때문에 이전 버전의 시스템을 배포하고싶으면 git revert와 같은 명령어를 사용하면 됩니다.

3. 승인된 변화는 자동으로 시스템에 적용됨
한 번 선언된 manifest가 Git에 등록되고 관리되기 시작하면 변화(코드수정 등)가 발생할때마다 자동으로 시스템에 적용되어야 하며, 클러스터에 배포할때마다 자격증명은 필요하지 않아야 합니다.

4. 배포에 실패하면 이를 사용자에게 경고해야 함
시스템 상태가 선언되고 버전 제어 하에 유지되었을 때 배포가 실패하게되면 사용자에게 경고할 수 있는 시스템을 마련해야합니다.

#### GitOps Repository

GitOps Pipeline을 설계할때에는 Git Repository를 최소 두개이상 사용하는 것을 권장합니다.

![image](https://user-images.githubusercontent.com/62640332/156988554-a40ee1c4-0beb-4239-a218-4b0e7f7e171b.png)


- App Repo : App 소스코드와, 배포를 위한 Manifest 파일
- 배포 환경 구성용 Repo : 배포 환경에 대한 모든 Manifest (모니터링, 서비스, MQ 등)들이 어떤 버전으로 어떻게 구성되어있는지 포함



### GitOps 배포 전략

1. Push Type
Git Repo가 변경되었을 때 파이프라인을 실행시키는 구조입니다.

![image](https://user-images.githubusercontent.com/62640332/156988660-b72954e5-203f-4406-90c0-ab4640ee2775.png)

배포 환경의 개수에 영향을 받지 않으며 접속 정보를 추가하거나 수정하는 것만으로도 간단하게 배포 환경을 추가하거나 변경할 수 있습니다.

아키텍처가 쉬워 많은 곳에서 사용하고 있으나, 보안정보가 외부로 노출될 수 있다는 단점이 있습니다.

2. Pull Type

배포하려는 클러스터에 위치한 별도의 오퍼레이터가 배포역할을 대신합니다.

![image](https://user-images.githubusercontent.com/62640332/156988759-b24af79c-2942-470b-96d9-7720ee23df87.png)

해당 오퍼레이터는 Git Repo의 Manifest와 배포환경을 지속적으로 비교하다가 차이가 발생할 경우, Git Repo의 Manifest를 기준으로 클러스터를 유지시켜 줍니다.

또한 Push Type과 달리 오퍼레이터가 App과 동일한 환경에서 동작중이므로 보안 정보가 외부에 노출되지 않고 실행할 수 있습니다.


### ArgoCD란?


버네티스를 위한 CD(Continuous Delivery)툴입니다.

GitOps방식으로 관리되는 Manifest 파일의 변경사항을 감시하며, 현재 배포된 환경의 상태와 Git에 정의된 Manifest 상태를 동일하게 유지하는 역할을 수행 합니다.

push타입과 pull타입 모두를 지원하며 pull타입 배포를 권장하고 있습니다.

### 한줄정리

- 쿠버네티스의 구성요소들을 관리하고 배포하기 위해서는 Manifest파일을 구성하여 실행해야하는데 이러한 파일들은 계속해서 변경되기 때문에 지속적인 관리가 필요한데 이를 편하게 Git으로 관리하는 방식 -> GitOps

- GitOps를 실현시키며 쿠버네티스에 배포까지 해주는 툴 -> ArgoCD

출처] https://gruuuuu.github.io/cloud/argocd-gitops/