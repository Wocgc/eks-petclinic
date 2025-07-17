# 🚀 EKS 기반 GitOps 애플리케이션 배포 구성 (Argo CD)

---

## 📌 개요

이 레포는 AWS EKS 클러스터에서 Argo CD 기반 GitOps 방식으로 애플리케이션을 배포 구성
Helm, Kustomize, Raw YAML을 조합하여 다양한 리소스를 배포하며, CI 파이프라인으로부터 전달받은 이미지 태그 변경도 자동 반영함함

---

## 🧰 사용 기술

- **Argo CD**
- **Kustomize**
- **Helm**
- **Raw Kubernetes YAML**
- **GitHub Actions** (GitOps 트리거 목적)
## 🖼️ 아키텍처 구성도

![architecture](docs/architecture.png)

## 🧱 전체 기술 스택

- IaC: Terraform
- CI: GitHub Actions
- CD: Argo CD (GitOps)
- Container Registry: ECR
- K8s Monitoring: Prometheus, Grafana
- Logging: EFK
---

## 🗂️ 폴더 구조

```bash
eks-petclinic/
├── app/             # Petclinic 앱 배포 정의 (CI가 이미지 태그 변경)
├── web/             # Web 프론트엔드 구성 (CI가 이미지 태그 변경)
├── monitoring/      # Prometheus, Grafana, Node Exporter 등
├── efk/             # Elasticsearch, Fluentd, Kibana 구성
├── ingress/         # ALB Ingress 설정 및 Helm values
├── hpa/             # HPA 정의 (CPU/Memory 기반 오토스케일링)
├── autoscaler/      # Cluster Autoscaler 설정
├── dashboard/       # Kubernetes Dashboard 배포
├── apps/            # Argo CD에서 사용하는 Application 선언들
├── role/            # IAM Role 및 정책 JSON
└── whatap/          # Whatap K8s Agent 설정
```

---

## 🧠 GitOps 구성 방식

| 항목 | 설명 |
|------|------|
| GitOps Tool | Argo CD |
| 앱 정의 방식 | Raw YAML or Helm |
| 앱 배포 경로 | `app/`, `web/`, `monitoring/` 등 |
| Argo CD 앱 정의 | `apps/` 아래 `.yaml` 파일로 각각 분리 |
| 이미지 자동 변경 위치 | `app/kustomization.yaml`, `web/kustomization.yaml` |
| 자동 커밋 소스 | [`petclinic-app`](https://github.com/Wocgc/petclinic-app) CI |
| Argo CD 설치 방식 | Helm Chart 사용 |

---

## 🔄 GitOps 동작 흐름

1. Petclinic CI가 Docker 이미지 빌드 및 ECR 푸시
2. `eks-petclinic/app/kustomization.yaml`의 `newTag:` 필드를 자동으로 수정
3. Git 커밋 후 push
4. Argo CD가 Git 변경 감지 → 자동으로 앱 재배포

---

## 🧪 연동된 CI 레포

```text
🔗 https://github.com/Wocgc/petclinic-app
→ CI에서 이미지 빌드 및 이 레포의 kustomization.yaml 자동 커밋
```

---

