# DevOps / DevSecOps Study Checklist (Week-by-week: exact topics to study)

Week 1 — Foundations, Git, Linux, Networking (study list)

Core (must know)
- Git
  - Commits, branches, merge vs rebase, fast‑forward vs non‑fast‑forward
  - Pull requests, code review workflow, protected branches, required checks
  - git revert, git reset (soft/mixed/hard), git cherry-pick, git bisect
  - .gitignore, submodules basics, git hooks (pre-commit)
- Linux
  - File permissions (u/g/o, chmod modes, ACLs), ownership (chown)
  - Systemd basics: systemctl status/start/stop/enable, journald (journalctl)
  - Processes: ps, top/htop, nice/renice, kill, strace basics
  - Disk: df, du, lsblk, mount; package managers apt/yum
  - Users/groups, sudo, ssh authorized_keys
- Networking
  - TCP vs UDP, 3‑way handshake, retransmissions, basic TCP tuning knobs
  - DNS resolution flow (stub resolver → recursive → authoritative), CNAME vs A record
  - HTTP (methods, status codes), TLS basics (cert chain, SNI)
  - Ports, NAT, CIDR notation, subnetting
- Scripting / automation
  - Bash basics: shebang, variables, conditionals, loops, functions, exit codes
  - Simple idempotent scripts, set -euo pipefail

Advanced (important for 2+ yrs)
- cgroups / namespaces basics (container primitives)
- Linux perf basics, iostat, vmstat
- tcpdump, ss/netstat basics for troubleshooting

Hands‑on tasks
- Create a repo and practice feature branch → PR → squash merge
- Write a Bash script to provision a user, create SSH key, install nginx, log output
- Use tcpdump + curl to trace an HTTP request locally

Week 2 — Docker (study list)

Core
- Container concepts: image vs container, union file systems (overlay), layers
- Dockerfile instructions and semantics: FROM, RUN, COPY vs ADD, WORKDIR, ENV, ARG, ENTRYPOINT, CMD
- Multi‑stage builds to shrink images
- Volumes vs bind mounts vs tmpfs
- Container networking: default bridge network, custom bridge, port mapping
- Docker Compose: service definitions, depends_on, healthcheck, networks
- Image registries and tags: tagging, pushing/pulling, immutable tags best practice

Advanced
- Image hardening: reduce layers, use distroless/minimal images, remove build deps
- Rootless containers, seccomp profiles, AppArmor basics
- SBOM concepts, image signing (cosign)
- Docker storage drivers, overlay2 internals

Hands‑on tasks
- Write a multi‑stage Dockerfile for a simple app (Node/Python/Go) and build image
- Create docker-compose.yaml for app + DB + redis; add healthchecks and volumes
- Scan built images with Trivy and fix at least one vulnerability

Week 3 — Terraform fundamentals (study list)

Core
- HCL syntax: resource, provider, variable, output, data
- terraform CLI: init, plan, apply, destroy, fmt, validate
- State: .tfstate structure, sensitive attributes, locking importance
- Providers and provider versions
- Variables (types: string, list, map, object), interpolation, locals
- Resource lifecycle meta-arguments: depends_on, create_before_destroy, prevent_destroy

Advanced / ops
- Remote backends (S3 + DynamoDB locking, Terraform Cloud): configuration and state locking
- terraform import, state list/show/pull
- Workspaces concept vs separate state files
- Basic state recovery & drift detection approaches

Hands‑on tasks
- Create VPC + subnet + 2 VMs + security group in your chosen cloud with Terraform
- Configure remote state backend (S3 + DynamoDB) and run plan/apply with locking
- Import an existing cloud resource into Terraform

Week 4 — Terraform advanced & testing (study list)

Core
- Modules: module architecture, inputs/outputs, nested modules, version pinning
- count vs for_each; when to use which; dynamic blocks
- Error handling patterns; sensitive values
- tflint, terraform validate, terraform fmt

Advanced
- Terratest (Go) or kitchen-terraform for integration tests
- Policy as code: OPA/Conftest / Sentinel basics and sample policies (tag enforcement, instance-size limits)
- State migration: terraform state mv, state rm, workspace migration strategies
- Secrets handling: avoid storing plaintext secrets in state; use remote secrets (Vault, KMS) or data sources

Hands‑on tasks
- Build a reusable network module and a compute module; publish locally and version tag
- Add a tflint config and a Conftest policy to fail builds missing required tags
- Write one Terratest that validates a module creates expected outputs (if learning Go is heavy, write kitchen/integration smoke tests)

Week 5 — Kubernetes fundamentals (study list)

Core
- API objects: Pod, ReplicaSet, Deployment, StatefulSet, DaemonSet, Service, Ingress, ConfigMap, Secret
- Pod lifecycle: init containers, readiness vs liveness probes, restartPolicy
- Services: ClusterIP, NodePort, LoadBalancer; Ingress basics and controllers (nginx/contour)
- Storage: PersistentVolume (PV), PersistentVolumeClaim (PVC), StorageClass
- Namespaces and resource quotas
- RBAC basics: Role, ClusterRole, RoleBinding, ServiceAccount

kubectl mastery
- kubectl get/describe/logs/exec/port-forward/rollout history/rollout undo
- kubectl apply vs kubectl replace vs kubectl patch

Hands‑on tasks
- Create a local cluster (kind/minikube/k3d) and deploy a 3-tier app (frontend/back/backend DB)
- Add ConfigMap/Secret usage, persistent storage for DB, and expose via Ingress
- Simulate a failing pod and diagnose CrashLoopBackOff

Week 6 — Kubernetes advanced & ecosystem (study list)

Core
- StatefulSet, Jobs & CronJobs, DaemonSet detailed behavior
- Helm: chart structure, templates, values.yaml, hooks
- Kustomize overlays
- Cluster components: api-server, etcd, controller-manager, scheduler, kubelet
- CNI plugins: Calico, Cilium, Flannel — basic differences
- NetworkPolicy (ingress/egress rules) and common patterns

Advanced / ops
- Cluster provisioning options: managed (EKS/GKE/AKS) vs self-managed (kubeadm/kops)
- Observability: Prometheus metrics model, exporters, Grafana dashboards
- In-cluster logging: EFK/EFK alternatives, log retention/cost tradeoffs
- Pod Security Standards, admission controllers, OPA Gatekeeper

Hands‑on tasks
- Create a Helm chart for your app, publish locally, and deploy with values overrides
- Implement NetworkPolicy limiting traffic between namespaces
- Install Prometheus + Grafana and create a dashboard for HTTP latency

Week 7 — CI/CD, GitOps, and pipelines (study list)

Core
- CI fundamentals: build/test/publish/deploy stages, caching, artifacts, secrets handling
- GitHub Actions (workflows), GitLab CI basics, Jenkins pipeline concepts
- Artifact registries: Harbor, Docker Hub, ECR/GCR/ACR basics
- GitOps principles: single source of truth, declarative desired state, reconcilers (Argo CD / Flux)

Security in pipelines
- SAST and SCA basics (tools: bandit, semgrep, OWASP dependency-check)
- Container scanning & SBOM integration
- Signing artifacts (cosign) and verifying at deploy time

Hands‑on tasks
- Create a CI pipeline that builds, tests, creates SBOM, signs, scans, and pushes an image
- Configure Argo CD to watch a Git ops repo and deploy to your cluster; simulate drift and reconcile

Week 8 — Observability, SRE, incident management (study list)

Core
- SLIs, SLOs, SLAs: how to define, measure, and act on error budgets
- Monitoring: metrics -> Prometheus scrape model, exporters, alert rules, alertmanager
- Logging: structured logs, correlation IDs, log aggregation, retention and index costs
- Tracing: OpenTelemetry basics, sampling, spans, traces, propagation

SRE / incident practice
- Pager vs alert differentiation; on-call best practices
- Runbooks, postmortem structure, RCA methodology (5 whys, fishbone)
- Chaos engineering basics (chaos experiments, game days)

Hands‑on tasks
- Define and implement SLOs for a sample service; create alerts and dashboards
- Run a simulated incident and produce a postmortem with actionable remediation

Week 9 — Security & compliance (study list)

Core
- Threat modeling basics (STRIDE/PASTA), attack surface review
- Secrets lifecycle: Vault basics, KMS integration, secret rotation strategies
- IAM best practices: least privilege, roles, service accounts, ephemeral creds
- Vulnerability management: scanning frequency, triage, patching cadence

Advanced / compliance
- Supply chain security: SBOMs, cosign/rekor, provenance
- Runtime protection: Falco, runtime EDR concepts
- Compliance mapping: basic controls for PCI/GDPR/HIPAA and how infra supports them

Hands‑on tasks
- Integrate Vault (or cloud KMS + secrets) and inject secrets into apps; test rotation
- Create an SBOM during CI and verify signatures before deploy

Week 10 — System design, interviewing, and polish (study list)

Core
- High availability: multi-AZ design, failover patterns, data replication strategies
- Deploy strategies: blue/green, canary, rolling, traffic splitting, feature flags
- Disaster Recovery: backup/restore, RPO/RTO, cross-region failover patterns
- Cost optimization basics: reserved instances, right-sizing, autoscaling strategies

Interview prep & soft skills
- Prepare STAR stories for: incident ownership, production fixes, architecture tradeoffs, mentoring
- One‑page diagrams for your projects and runbooks you can show live
- Timed practice: terraform plan & apply target infra in 45–60 minutes; k8s debug in 15–20 minutes

Hands‑on tasks
- Do 3 timed mock interviews (CLI infra task, k8s debugging, design whiteboard)
- Finalize portfolio repo (README, diagrams, runbooks, sample CI YAMLs, module links)

Quick reference — must‑know commands & resources
- Terraform: terraform init/plan/apply/taint/state list/import; read hashicorp learn tutorials
- Docker: docker build/run/exec/ps/logs; docker-compose up/down
- K8s: kubectl get/describe/logs/exec/port-forward/rollout; helm install/upgrade
- Git: git branch/checkout/rebase/merge/push/pull
- CI/CD: read GitHub Actions and Argo CD quickstarts

Study & practice cadence suggestions
- Daily: 30–90 min hands-on + 30 min reading (docs or blog) + 10–15 min notes
- Weekly: one timed hands-on exam (deploy + demo) and one mock interview
- Keep artifacts: small repos, diagrams (draw.io), runbooks, and recorded demos
