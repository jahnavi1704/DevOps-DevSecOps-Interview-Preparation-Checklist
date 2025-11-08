# Senior (2+ years) DevOps / DevSecOps Interview Prep — 10-week Plan & Checklist

Short answer about guarantees
- No guarantees: interviews depend on role scope, company, and interpersonal factors.
- What this plan does: aligns your knowledge, hands-on deliverables, and interview practice to match what companies expect from candidates with 2+ years of DevOps/DevSecOps experience (system design, production ownership, security, SRE practices).

How to use this
- Follow the 10-week plan. Each week lists must-cover topic titles, hands-on tasks, and checkpoints.
- Build deliverables (repos, PRs, runbooks, diagrams). These are evidence you can show during interviews.
- Do mock interviews (technical + system design + behavioral) and timed hands-on exercises.

Time commitment
- Target: 12–25 hours/week (intensive). If you have less time, extend the timeline and prioritize projects and mock interviews.

Overview of what distinguishes 2+ years candidates
- Demonstrable ownership of production services (deployments, incidents, runbooks)
- Understanding of architecture & trade-offs at scale (HA, multi-AZ/region, DR)
- Expertise with Terraform/Docker/K8s plus patterns for testing, modularization, and state management
- Ability to design secure pipelines and operationalize security (SCA, SAST, runtime)
- SRE mindset: SLIs/SLOs, incident management, postmortems, capacity planning
- Soft skills: clear explanations, stakeholder communication, mentorship examples

10-week plan (senior / 2+ years focus)

Week 1 — Foundations + Evidence collection
- Must-cover topics
  - Git advanced workflows: trunk-based, release branching, protected branches, CI gate rules
  - Linux: kernel tuning basics, cgroups, namespaces, system troubleshooting (dmesg, journalctl, perf basics)
  - Networking: TCP tuning, load balancer behavior, health checks, TLS termination, DNS at scale
  - Documentation & artifacts: how to write runbooks, architecture diagrams, README best practices
- Hands-on
  - [ ] Create a "portfolio" repo listing projects, diagrams, runbooks and the checklist
  - [ ] Write a runbook for "deploy rollback" and "high CPU incident" (real or simulated)
- Checkpoint: Can present a one-page architecture diagram and two runbooks

Week 2 — Docker (production & security)
- Must-cover topics
  - Image hardening, reproducible builds, SBOM basics, image signing (cosign)
  - Multi-stage & reproducible caching, CI build optimization
  - Runtime security: seccomp, AppArmor, user namespaces, rootless containers
  - Registries: retention policies, immutability, cleanup
- Hands-on
  - [ ] Dockerize a service with CI-built, signed image + SBOM; add Trivy scan and block on criticals
  - [ ] Demonstrate rootless container run and a minimised base image
- Checkpoint: Explain image trust chain and how to manage supply chain risks

Week 3 — Terraform (ops-grade)
- Must-cover topics
  - Module design for teams, versioning & release process, composition patterns
  - Remote state design at scale (S3 + DynamoDB, locking strategy), state security and encryption
  - Safe change strategies: blue/green infra, resource replacement patterns, drift detection
  - Terragrunt/monorepo vs multi-repo patterns (pros/cons)
- Hands-on
  - [ ] Build production-grade reusable modules (network + compute + infra components), tag versions
  - [ ] Implement remote state with locking and a CI pipeline that performs plan & apply safely
- Checkpoint: Walk through an unsafe change and how you'd prevent it

Week 4 — Terraform advanced tooling & testing
- Must-cover topics
  - Policy-as-code (OPA/Conftest, Sentinel) integrated into CI
  - Automated testing: Terratest (Go) or kitchen-terraform, unit/integration patterns
  - State surgery: resource move, import, state recovery scenarios
  - Secrets: avoid secret leakage in state, remote secret sources (Vault/KMS)
- Hands-on
  - [ ] Add policy checks for tags, instance sizes; add Terratest tests for modules
  - [ ] Simulate state corruption and document recovery steps
- Checkpoint: Run CI that lints, tests, and policies Terraform before apply

Week 5 — Kubernetes (operational mastery)
- Must-cover topics
  - Cluster lifecycle: provisioning (managed vs self-managed), upgrades, backup/restore of etcd
  - Observability at scale: metrics, distributed tracing, logging strategy, cardinality concerns
  - Storage in production: dynamic provisioning, snapshots, performance tuning
  - Security: Pod Security Standards, NetworkPolicy, admission controllers, image policies
- Hands-on
  - [ ] Provision a managed K8s (EKS/GKE/AKS) cluster via Terraform with node pools and autoscaling
  - [ ] Implement cluster upgrade and test application compatibility
- Checkpoint: Demonstrate cluster upgrade and show backup + restore for etcd or control-plane components

Week 6 — Kubernetes advanced patterns & service reliability
- Must-cover topics
  - Progressive delivery (Argo Rollouts, Istio or Linkerd for traffic routing)
  - Stateful workloads and operators (how operators manage stateful apps)
  - Cluster autoscaling patterns, binpacking, resource requests/limits, QoS classes
  - Service mesh tradeoffs, sidecar patterns, mTLS at scale
- Hands-on
  - [ ] Implement a canary deployment with traffic split and rollback policy
  - [ ] Tune HPA rules and cluster-autoscaler; demonstrate recovery from node loss
- Checkpoint: Explain decisions for using service mesh and autoscaler configuration

Week 7 — CI/CD at scale + GitOps
- Must-cover topics
  - Pipeline security: ephemeral runners, secret injection, least-privilege service accounts, artifact signing
  - GitOps workflows, repo layout, drift detection, multi-cluster promotion
  - Pipeline scalability, caching strategies, monorepo vs polyrepo CI considerations
  - Artifact registries lifecycle and retention
- Hands-on
  - [ ] Build a GitHub Actions/GitLab CI pipeline that builds, tests, signs, and publishes artifacts; deploy via Argo CD
  - [ ] Implement policy gate that blocks deploys lacking SBOM or vulnerability threshold
- Checkpoint: Present pipeline architecture and security controls

Week 8 — Observability, SLOs, and incident practice (SRE)
- Must-cover topics
  - Defining SLIs, SLOs, error budgets; alerting vs paging; playbook design
  - Logging strategy: structured logs, correlation IDs, retention/cost tradeoffs
  - Tracing: sampling strategies and instrumentation
  - Chaos engineering basics and game days
- Hands-on
  - [ ] Define SLOs for a service, create dashboards and alerts in Prometheus/Grafana, and test alerting
  - [ ] Run a game-day: induce pod failure and validate runbook/recovery
- Checkpoint: Show SLO dashboard and post-game-day notes with RCA

Week 9 — Security & Compliance (DevSecOps)
- Must-cover topics
  - Threat modeling; secure defaults; vulnerability triage & remediation process
  - Secrets lifecycle, key rotation, KMS/Vault integration, least privilege IAM
  - Compliance basics (PCI/GDPR/HIPAA) and how infra can be organized to meet controls
  - Runtime protection (Falco), supply-chain security (SBOM, cosign)
- Hands-on
  - [ ] Implement Vault-based secret injection and rotate a secret in a running service
  - [ ] Run a supply-chain audit: SBOM generation + signature verification in CI
- Checkpoint: Present threat model and remediation process for a sample service

Week 10 — System design, interviewing, and final projects
- Must-cover topics
  - System design for infra: multi-region HA, blue/green for stateful systems, DR planning
  - Behavioral & leadership stories: incident ownership, cross-team collaboration, mentoring
  - Mock interviews: hands-on timed tasks, design whiteboard, behavioral STAR responses
- Hands-on
  - [ ] Complete at least 2 end-to-end projects from infra → CI → observability → runbooks
  - [ ] Do 3 timed mock interviews (one CLI/terraform task, one k8s debugging task, one system design)
- Checkpoint: Can deploy baseline infra in 30–60 mins, explain tradeoffs, and present 3 production incidents and lessons learned

High-value projects (pick at least two)
- Production infra repo: Terraform modules + CI/CD + README + diagrams + tests
- GitOps deployment demo: Git repo for k8s manifests + Argo CD + promotion flow
- Secure pipeline: image signing, SBOM, Trivy/COSIGN integration, policy gating
- SRE demo: SLOs, alerting, game-day report, incident postmortem

Interview readiness rubric (senior / 2+ years)
- Technical (must): Build & explain infra in 45–60 minutes; debug k8s pod in 20 minutes; explain Terraform state, module design, and reclamation
- Systems thinking: Design multi-AZ HA, failover & DR, cost mitigation, autoscaling tradeoffs
- Security & compliance: Demonstrable pipeline and runtime protections; secret handling and SBOMs
- SRE & process: SLOs with alerts and playbooks; at least one real or simulated postmortem
- Behavioral: Clear STAR stories about ownership, tradeoffs, mentoring, and incidents
- Score yourself on each area; practice until you can explain each topic succinctly and show artifacts

Example senior interview questions to rehearse (topics)
- Design: "Design a multi-region, zero-downtime deploy for a stateful service"
- Terraform: "How do you structure Terraform for multiple teams across environments?"
- K8s ops: "How do you upgrade a K8s cluster with minimal disruption?"
- CI: "How do you secure build runners and secrets in CI?"
- SRE: "Define an SLO for a checkout flow and how you'd respond to breach"
- Security: "How do you implement supply-chain security for images?"

Deliverables you should produce
- Portfolio repo with 3–5 projects, README, and architecture diagrams
- Terraform modules with tests and version tags
- CI pipeline examples with security gates (YAML)
- Runbooks and at least one incident postmortem
- One-page "cheat" design notes for rapid interview reference

Resources & practice recommendations
- Keep reading HashiCorp, Kubernetes, and cloud provider docs; do KodeKloud / A Cloud Guru labs
- Record mock interviews and timebox tasks
- Pair with a peer or mentor for code reviews and mock interviews

Final notes
- This plan raises the bar to match 2+ years expectations: architecture, production, security, and SRE practices.
- Execution matters more than time: produce artifacts you can show and narrate.