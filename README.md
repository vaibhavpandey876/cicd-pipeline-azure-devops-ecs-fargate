# ⚙️ CI/CD Pipeline — Azure DevOps to AWS ECS Fargate

> 5 Repos | 4 Environments | Immutable Build Tagging
> 60% Faster Deployments | Zero "Which version is in prod?" questions

## 🔄 Pipeline Flow
Developer Push
↓
Azure DevOps Pipeline
↓
├── Unit Tests
├── Security Scan (Trivy)
├── Docker Build
└── Tag: {SERVICE}-{GIT_SHA}-{TIMESTAMP}
↓
AWS ECR Push (immutable tag)
↓
ECS Task Definition Update
↓
ECS Fargate Deploy (Blue/Green)
↓
Cloud Map Service Registry Update
## 🌍 Environments

| Environment | Trigger | Approval |
|---|---|---|
| int | Auto on feature branch | None |
| uat | Auto on merge to develop | None |
| live | Manual trigger | Tech Lead |
| client | Manual trigger | CTO |

## ⚙️ Tech Stack

| Component | Technology |
|---|---|
| CI/CD | Azure DevOps Classic |
| Container Registry | AWS ECR |
| Compute | AWS ECS Fargate |
| Service Discovery | AWS Cloud Map |
| Containerization | Docker |
| Deployment Strategy | Blue/Green |

## 🔑 Key Design Decisions

**Immutable Tags**
Every image tagged {service}-{git_sha}-{timestamp}.
No :latest anywhere. Every container traceable
to exact git commit.

**ECS Circuit Breaker**
Auto-rollback if 50%+ tasks fail health check.
No manual intervention needed.

**Cloud Map**
Services discover each other by name not IP.
ECS handles registration automatically on deploy.

## 📊 Results

- ✅ Deployment time reduced 60%
- ✅ 5 repos, 4 environments, single pipeline
- ✅ Every prod container linked to exact commit
- ✅ Rollback time under 3 minutes

## 🔑 Key Learning

Immutable tags changed everything —
:latest is a lie, a git SHA is the truth.
