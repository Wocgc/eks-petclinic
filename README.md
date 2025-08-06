# 🐾 eks-petclinic (GitOps 전용)

이 저장소는 AWS EKS 클러스터에 Spring Petclinic 애플리케이션을 GitOps 방식으로 배포하기 위한 Kubernetes 리소스 모음입니다.  
**Argo CD + Kustomize**를 활용하여 기능별로 리소스를 모듈화하고, 운영 자동화 및 선언적 배포 환경을 구축했습니다.

> 📌 이 레포는 **EKS GitOps 구성 전용**입니다.  
> - Terraform 기반 EKS 인프라: [infra-eks-terraform](https://github.com/Wocgc/infra-eks-terraform)  
> - Petclinic 애플리케이션 & CI 파이프라인: [eks-petclinic-app](https://github.com/Wocgc/petclinic-app)

---

## 🗂️ 디렉토리 구조

```bash
.
├── app/              # Spring App (Backend) 리소스
├── apps/             # Argo CD Application 정의 (GitOps 진입점)
├── autoscaler/       # Cluster Autoscaler (IRSA + Helm values 대응)
├── dashboard/        # Kubernetes Dashboard 설정
├── efk/              # Elasticsearch + Fluentd + Kibana 스택
├── hpa/              # HPA (Horizontal Pod Autoscaler)
├── ingress/          # ALB Ingress 설정 및 경로 기반 라우팅
├── monitoring/       # Prometheus + Grafana 구성
├── role/             # IAM Role for ServiceAccount (IRSA)
├── test/             # 테스트 리소스 (deprecated)
├── web/              # Spring Web (Frontend) 리소스
├── whatap/           # Whatap APM 연동 (선택적)
├── .argocdignore     # Argo CD 무시 대상 정의
└── .gitignore        # Git 무시 파일

🧩 적용 기술 스택
| 구성 요소       | 기술                                   |
| ----------- | ------------------------------------ |
| Kubernetes  | Amazon EKS                           |
| GitOps      | Argo CD + Kustomize                  |
| CI          | GitHub Actions                       |
| Ingress     | ALB Ingress Controller + ExternalDNS |
| Monitoring  | Prometheus + Grafana                 |
| Logging     | Elasticsearch + Fluentd + Kibana     |
| Autoscaling | HPA + Cluster Autoscaler (IRSA)      |
| APM (옵션)    | Whatap                               |
| 인증 및 보안     | IRSA, RBAC, ACM, TLS                 |


✅ 특징 요약
🔄 Git 변경사항 → Argo CD 자동 배포

📦 리소스 기능별 모듈화 (app/web/monitoring 등)

⚙️ Kustomize 기반 버전 관리와 오버레이 대응

🔐 IAM Role for Service Account(IRSA) 기반 최소 권한 구성

📈 실시간 모니터링 및 로그 수집까지 통합 관리
