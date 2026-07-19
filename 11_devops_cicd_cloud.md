# 11 — DevOps, CI/CD & Cloud

> **Module rating:** ★★★★☆ (High ROI) · **Difficulty:** Intermediate → Advanced · **Est. effort:** 1–1.5 weeks · **Depth target:** Production (run + debug), not platform administration
> **Prerequisites:** [Build tooling](12_build_tooling.md), [Spring Boot](3_spring_and_spring_boot.md), [Observability](8_observability_monitoring_logging.md).
> **Nav:** [◀ Performance](10_performance_profiling_reliability.md) · [Next ▶ Build & Tooling](12_build_tooling.md) · **Related:** [Microservices](5_microservices_distributed_systems.md), [Cloud secrets/KMS](16_misc_nice_to_have.md)

---

## Why this module

The "backend engineer who just writes APIs" is gone. In 2026 you're expected to **containerize, deploy, and debug** your service in Kubernetes and understand the CI/CD path — enough to be self-sufficient, not to own the platform. Backend owns "code that runs in the cluster and emits metrics"; DevOps owns the cluster itself.

> **Scope guardrail:** you need K8s to *run and debug*, Terraform to *read and modify*, and one cloud (AWS) at a *fundamentals* level. Don't rabbit-hole into full DevOps.

---

## Core

### Docker — ★★★★☆ · Intermediate · 1 day
- **What exactly:** images vs containers, Dockerfile, **multi-stage builds** (small final image), layer caching, `.dockerignore`, non-root user, distroless/slim base, JVM-in-container ergonomics (respect cgroup memory/CPU limits), image scanning.
- **Interview Qs:** "why multi-stage builds?"; "how do you shrink a Java image?"; "why did the JVM OOM in a container with a memory limit?" (heap not sized to cgroup / old JVMs).
- **Red flags:** giant images; running as root; secrets baked into layers.

### Kubernetes essentials — ★★★★☆ · Intermediate → Advanced · 3 days
- **What exactly:** pods, Deployments vs StatefulSets, Services, ConfigMaps/Secrets, **liveness/readiness/startup probes**, resource requests/limits, HPA, rolling updates + rollbacks, namespaces; **debugging**: `kubectl logs/describe/exec`, `CrashLoopBackOff`, `OOMKilled`, `ImagePullBackOff`, pending pods (resources).
- **How deeply:** Production — deploy + debug your own service.
- **Interview Qs:** "Deployment vs StatefulSet?"; "liveness vs readiness probe — what breaks if you misuse them?" (liveness restarts a healthy-but-busy pod → cascading restarts); "how do you debug `CrashLoopBackOff`?"; "what causes `OOMKilled`?"
- **Red flags:** no resource limits; liveness probe that restarts under load; no readiness gate during rollout.

### CI/CD — ★★★★☆ · Intermediate · 1 day
- **What exactly:** pipeline stages (build → test → scan → image → deploy), **GitHub Actions** (workflows, caching, matrix), artifact/versioning, blue-green vs canary vs rolling, secrets in CI, gated deploys.
- **Interview Qs:** "design a CI/CD pipeline for a microservice"; "canary vs blue-green?"; "how do you roll back a bad deploy?"
- **Related:** [Testing in CI](9_testing_quality.md).

### Cloud fundamentals (AWS primary) — ★★★★☆ · Intermediate · 2 days
- **What exactly:** compute (EC2/ECS/EKS/Lambda), storage (S3, EBS), managed DB (RDS), networking (VPC/subnets/SG basics), **IAM** (roles, least privilege), secrets (Secrets Manager/Parameter Store), load balancers, multi-AZ.
- **Interview Qs:** "how does IAM role-based access work?"; "when ECS vs EKS vs Lambda?"; "how do you give a pod/app access to S3 without hardcoded keys?" (IAM roles / IRSA).
- **Red flags:** hardcoded credentials; overly broad IAM policies; single-AZ for critical data.

### Infrastructure as Code — ★★★☆☆ · Intermediate · 1 day
- **What exactly:** Terraform basics (providers, resources, state, plan/apply, modules), read/modify existing IaC, immutable infra concept.
- **Interview Qs:** "why IaC?"; "what is Terraform state and why does it matter?"

## Situational
- **Helm — ★★★☆☆:** templating/packaging K8s manifests; read + tweak charts.
- **GitOps / ArgoCD — ★★☆☆☆:** declarative deploys from Git; awareness.
- **Serverless (Lambda) — ★★☆☆☆:** event-driven, cold starts, cost model; situational.
- **Service mesh — ★★☆☆☆:** see [Microservices](5_microservices_distributed_systems.md).

---

## Hands-on labs & failure scenarios

- **Lab 1:** write a multi-stage Dockerfile for your Spring Boot app; get the image under ~200MB; run as non-root.
- **Lab 2:** deploy to a local K8s (kind/minikube) with probes + resource limits + HPA; roll out a new version and roll it back.
- **Lab 3:** build a GitHub Actions pipeline: build → test (Testcontainers) → image → push.
- **Failure scenario:** your pod is in `CrashLoopBackOff` — walk the diagnosis (`describe`, `logs`, exit code, OOMKilled?) and fix.
- **Debugging task:** JVM `OOMKilled` in a 512Mi pod though `-Xmx` looked fine — fix heap sizing vs cgroup limit.

---

## Checklists

### Interview Checklist
- **Must know:** Docker multi-stage + JVM-in-container; Deployment vs StatefulSet; probes; resource limits; `CrashLoopBackOff`/`OOMKilled` debugging; CI/CD stages + rollback; IAM least privilege; deploy strategies.
- **Good to know:** HPA; Terraform state; Helm; ECS vs EKS vs Lambda.
- **Bonus:** GitOps/ArgoCD; IRSA; canary automation.

### Production Checklist
- **Must know:** resource limits set; probes correct; secrets externalized; images scanned + non-root; rollbacks tested.
- **Good to know:** autoscaling policies; multi-AZ; least-privilege IAM.

### Hands-on Checklist
- **Must:** containerized + deployed a service to K8s with probes; built a CI pipeline.
- **Good:** performed a rollback; debugged a CrashLoopBackOff.
- **Bonus:** provisioned infra with Terraform.

---

## Detailed Syllabus (topic checklist)

> Full topic inventory for reference (scoped to what a backend engineer needs, not platform admin). Priorities/depth are in the guide above.

**1. DevOps fundamentals**
- Culture (ownership, you-build-it-you-run-it); Infrastructure as Code mindset

**2. CI/CD pipelines**
- Stages: build → test → package → deploy; artifact/versioning
- Tools: GitHub Actions (primary), GitLab CI, Jenkins, CircleCI
- Deployment strategies: blue-green, canary, rolling; feature flags → see [Misc](16_misc_nice_to_have.md)

**3. Containers**
- Docker: images, containers, volumes, networks; Dockerfile; multi-stage builds
- JVM-in-container: memory/CPU limits, `-XX:MaxRAMPercentage`, ergonomics; small base images (distroless/jlink)

**4. Kubernetes essentials (debug-focused)**
- Pods, deployments, services, ingress, configmaps, secrets
- Liveness/readiness/startup probes; resource requests/limits; HPA
- Debugging: `CrashLoopBackOff`, `OOMKilled`, pending pods, `kubectl logs/describe/exec`
- Helm charts (awareness)

**5. Cloud platforms (AWS-first)**
- Core services: compute (EC2/ECS/EKS/Lambda), storage (S3/EBS), databases (RDS/DynamoDB), networking (VPC/ALB/Route53)
- IAM (roles, policies, least privilege); serverless (Lambda) basics
- GCP/Azure equivalents (awareness)

**6. Infrastructure as Code**
- Terraform basics (providers, resources, state); CloudFormation / Ansible (awareness); GitOps (ArgoCD/Flux — awareness)

**7. Security & monitoring in DevOps**
- Secrets management & scanning; image/dependency scanning (SCA); cloud monitoring (CloudWatch)

**8. Interview**
- Explain a CI/CD workflow; Docker vs Kubernetes; how you'd debug a crashing pod; handling secrets in pipelines; zero-downtime deploys

---

**Nav:** [◀ Performance](10_performance_profiling_reliability.md) · [Next ▶ Build & Tooling](12_build_tooling.md)
