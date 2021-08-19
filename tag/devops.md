# Devops KT

## ArgoCD

- Gitops Repository(kubernetes에서 사용할 manifest resource yaml 파일들을 관리하는 repository)의 내용을 감지하여 
  내용의 변경사항(Diff)이 발견되면 이를 사용자에게 알려주고 반영할지 여부를 체크

## Kustomize

- kubernetes resource 에 대한 정의서(manifest)를 환경에 맞게 customize하여 배포할 수 있는 도구이며 base와 overlay로 나눔
- 공통된 부분은 base, 환경마다 차이가 발생하는 부분을 overlay라는 항목으로 분리하는 개념에서 시작한다. 
  각각의 환경에 배포할 때, 이 base와 overlay의 Manifest 파일을 merge하여 환경마다 서로 다른 Spec의 리소스를 생성

## blue-green in k8s

- Deployment와 Service를 추가하고, Service의 selector의 이름을 변경하는 방법


## SLI/SLO/SLA

- SLI(Service Level Indicator)는 서비스 수준을 판단할 수 있는 기준 몇가지를 정량적으로 측정한 값이며 측정할때는 단위의 표준화가 필요
  - 시스템 가용성, 응답시간, 처리량, 에러율 등
  - 데이터의 수집 주기는 10초 단위로 하고, 범위는 서비스 클러스터 단위로 한다 등

- SLO(Service Level Objectives)는 서비스 수준 목표를 의미하며, SLI에 의해 측정된 서비스 수준의 목표 값 또는 일정 범위
  - SLO = SLI + 목표값
  - 매주, 99% of REST API 호출의 응답 시간은 100ms 이하여야 한다.
  - 단순하고 현실성 있는 목표치를 설정하고 가능한 적은 수로 설정 

- SLA(Service Level Agreement)는 고객이 공급업체에게 기대하는 서비스 수준을 기술한 문서
  - 99.999 퍼센트의 네트워크 가용성

## 금융/보험 클라우드 환경

- 하이브리드 클라우드 환경 도입
  
- 시스템 안정성 확보
  - 계정관리 (IAM, Organizations)
  - 접근통제 (망분리, VPC, SG, 네트워크 보안)
  - 암호화 및 키관리 (KMS, Cloud HSM)
  - 가상환경 모니터링 (CloudTrail, CloudWatch
  - 이미지 보안패치 (System Manager)
  - 보안 모니터링 (WAF, Shield, CloudFront)

- 업무 연속성 확보
  - 데이터 백업 (S3, Snapshot, RDS)

- 보안사고 대응체계
  - 인프라 및 데이터보호 (Security Hub, Amazon Macie, GuardDuty)

- 사용자의 개입이 적은 시스템 구성
  - DevSecOps, CloudFormation, Terraform

## CIDR (Classless Inter-Domain Routing)

- 클래스 없는 도메인간 라우팅 기법으로 IP주소 할당방법
- VPC IP대역 예
  - A Class 10.0.0.0/8
  - B Class 172.16.0.0/12000        
  - C Class 192.168.0.0/16 (192.168.0.0 ~ 192.168.255.255) - 65536개
    - 192.168.0.0/20 (192.168.0.0 ~ 192.168.15.255) - 4096개

## AWS Networking

- VPC (Virtual Priavte Cloud)
  - 사용자가 정의한 가상 네트워크로 내부에 각종 Resource를 만들 수 있음
- Subnet
  - VPC 내부를 쪼개서 사용 public과 private으로 구성
- Routing Table
  - 목적지에 대한 정보를 담고있는 테이블
- Route 53
  - 관리형 DNS 서비스
  - 기본적인 DNS 서비스 외에 추가로 LB Routing, Failover, round robin 등의 기능도 제공
  - A Record : 도메인과 IP 주소 매핑,  CNAME : 도메인 연결
- CloudFront
  - 전 세계에 파일을 빠른 속도로 배포하는 CDN 서비스
  - 전 세계 주요지역의 엣지 로케이션에 존재
  - S3 Bucket, EC2 instance, ELB, 기타 웹서버 지원
- Internet Gateway
  - VPC의 인스턴스와 인터넷 간의 통신을 제공
  - 해당 인스턴스는 공인 IP를 보유하고, 인스턴스가 있는 Subnet의 Routing table에 등록되어야 함
- NAT(Network Address Translation)
  - Private Network에 속한 여러 개의 호스트가 하나의 공인 IP주소를 사용하여 인터넷에 접속하기 위해 주로 사용
- NAT Gateway
  - Private Subnet 인스턴스들의 외부로부터의 접속은 차단하면서 단방향으로 업데이트 등의 인터넷 접속이 필요할 때 사용
  - Public Subnet에 NAT Gateway를 만들고 공인IP를 만들어 Private Subnet과 연결함
- Security Group
  - 인스턴스에 대한 인바운드 및 아웃바운드 트래픽을 제어하는 가상 방화벽
  - 한번 인바운드/아웃바운드를 통과하는 트래픽은 아웃/인바운드 규칙 적용 바받지 않음 (Stateful)
- Network ACL
  - 서브넷 단위로 오고 가는 트래픽을 제어
- VPC Flow Logs
  - VPC, Subnet 또는 네트워크 인터페이스에 대한 흐름 로그를 생성
  - VPC 내 Resource들은 모두 Elastic Network Interface (ENI)를 가지고 있음
- VPC Endpoint
  - VPC 내부 Resource가 VPC 외부 AWS 서비스와 통신할때 외부 인터넷을 거치지 않고 전용 연결을 통해 도달하게 함
  - Gateway Endpoint : S3, Dynamo DB 는 자동으로 routing 추가

## Network ACL vs Security Group
- Security Group
  - 인스턴스 기준 (1차)
  - 룰에 대한 허용규칙만 지원
  - 아웃바운드 요청 응답 자동 허용 (stateful)
  - 등록된 모든 룰을 평가 
- Network ACL
  - 서브넷 기준 (2차)
  - 룰에 대한 허용 및 거부규칙 지원
  - 아웃바운드 요청 응답 규칙 정의 필요 (stateless)
  - 번호가 낮은 규칙부터 순서대로 트래픽 허용/거부
  - 설정된 서브넷 하단의 모든 인스턴스 적용
- 바람직한 사용법
  - Security Group에는 허용되어야 할 프로토콜과 포트를 지정 (IP x)
  - Network ACL에는 모든 트래픽을 허용하되, 차단할 필요가 있는 IP 차단

