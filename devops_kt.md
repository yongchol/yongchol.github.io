# ArgoCD

- Gitops Repository(kubernetes에서 사용할 manifest resource yaml 파일들을 관리하는 repository)의 내용을 감지하여 
  내용의 변경사항(Diff)이 발견되면 이를 사용자에게 알려주고 반영할지 여부를 체크



# Kustomize

- kubernetes resource 에 대한 정의서(manifest)를 환경에 맞게 customize하여 배포할 수 있는 도구이며 base와 overlay로 나눔
- 공통된 부분은 base, 환경마다 차이가 발생하는 부분을 overlay라는 항목으로 분리하는 개념에서 시작한다. 
  각각의 환경에 배포할 때, 이 base와 overlay의 Manifest 파일을 merge하여 환경마다 서로 다른 Spec의 리소스를 생성

# blue-green in k8s

- Deployment와 Service를 추가하고, Service의 selector의 이름을 변경하는 방법


# SLI/SLO/SLA

- SLI(Service Level Indicator)는 서비스 수준을 판단할 수 있는 기준 몇가지를 정량적으로 측정한 값이며 측정할때는 단위의 표준화가 필요
  - 시스템 가용성, 응답시간, 처리량, 에러율 등
  - 데이터의 수집 주기는 10초 단위로 하고, 범위는 서비스 클러스터 단위로 한다 등

- SLO(Service Level Objectives)는 서비스 수준 목표를 의미하며, SLI에 의해 측정된 서비스 수준의 목표 값 또는 일정 범위
  - SLO = SLI + 목표값
  - 매주, 99% of REST API 호출의 응답 시간은 100ms 이하여야 한다.
  - 단순하고 현실성 있는 목표치를 설정하고 가능한 적은 수로 설정 

- SLA(Service Level Agreement)는 고객이 공급업체에게 기대하는 서비스 수준을 기술한 문서
  - 99.999 퍼센트의 네트워크 가용성

# 금융/보험 클라우드 환경

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

