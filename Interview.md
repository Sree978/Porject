Q1 Behavioural  --  Tell me about yourself and your DevOps experience.
Your answer  :
I'm a DevOps Engineer at TCS with 4 years of experience, where I've been supporting Bank of Montreal — a Tier-1 
global banking client — on production AWS infrastructure. Day-to-day I manage EKS clusters, 
Terraform IaC across 3 AWS accounts, GitLab CI/CD pipelines, and full-stack observability with Grafana, 
Dynatrace, and CloudWatch. I've helped reduce deployment cycle time by 40%, cut provisioning time by 60%, 
and delivered 20–25% cloud cost savings. I thrive in high-stakes, zero-tolerance environments where uptime 
and security are non-negotiable.
Q2
Technical
Walk me through how you manage Kubernetes workloads in production.
Your answer
I manage Amazon EKS clusters with IRSA for pod-level IAM, ALB Ingress Controller for routing across 
15+ microservices, and Kubernetes RBAC for access control. I deploy applications using Helm charts 
integrated into our GitLab CI/CD pipeline — so every release is versioned and reproducible. 
For scaling, I use HPA based on CPU and custom metrics. For zero-downtime releases I use rolling
update strategy with readiness probes configured. During incidents I use kubectl describe, logs, 
and events alongside Grafana dashboards to isolate pod-level issues. For BMO we maintain 99.9%+ 
availability across all environments.

Q3
Technical
How do you manage Terraform at scale across multiple environments?
Your answer
I use modular Terraform with separate modules for networking, compute, and security. I manage 
3 AWS accounts — dev, staging, and production — using Terraform workspaces for environment isolation.
Remote state is stored in S3 with DynamoDB for state locking to prevent concurrent modifications. 
I enforce no manual changes through strict GitLab CI/CD pipelines that run terraform plan on every 
merge request and terraform apply only on approval to main. This eliminated config drift and reduced 
provisioning time by ~60%. I also use variable files per environment to keep modules DRY.

Q4
Situational
Describe a production incident you handled. What was your process?
Your answer
We had a P1 incident where payment-processing pods on EKS were OOMKilled, causing API errors for end users. 
I immediately checked Grafana and Dynatrace to confirm spike in memory consumption, then pulled kubectl 
describe pod to see OOMKilled events. I rolled back the Helm release while simultaneously checking recent 
code changes in GitLab. Root cause was an unoptimized database query introduced in the last release
that caused memory leak under load. I patched the query, redeployed via pipeline, and confirmed
metrics stabilised. Total resolution time was under 30 minutes. Post-incident I added memory alerts 
at 80% threshold and introduced load testing gates in the pipeline.
Q5
Technical
How do you approach CI/CD pipeline design for zero-downtime deployments?
Your answer
Our GitLab CI/CD pipeline follows: build → unit test → Docker image build → push to ECR → Helm upgrade 
to EKS. For zero-downtime I configure rolling update strategy in Kubernetes with maxUnavailable: 0 
and proper readiness probes so traffic only routes to healthy pods. Automated rollback is triggered 
if the deployment health check fails within a defined window. I've also set up self-hosted GitLab 
runners on Kubernetes with horizontal auto-scaling, which cut CI build queue wait times by ~50% during 
peak windows. For high-risk releases I advocate blue-green or canary patterns so we can shift 
traffic gradually.
Q6
Technical
How do you handle observability and alerting for microservices?
Your answer
I've built full-stack observability across 10+ microservices using a combination of Prometheus for metrics,
Grafana for dashboards with custom SLI/SLO panels, Dynatrace APM for traces and application-level insights, 
and AWS CloudWatch for infrastructure-level logs and alarms. I set up SNS-based multi-channel 
alerting — email, Slack, PagerDuty — for 50+ critical metrics. This reduced mean alert-to-acknowledge 
time from 15 minutes to under 2 minutes, and our overall MTTR dropped by ~30%. For SLO tracking 
I define error budgets and alert when we're burning through them faster than allowed.
Q7
How do you ensure security in your AWS infrastructure?
Your answer
Security is layered across our stack. At the identity layer I use IAM with least-privilege policies 
and IRSA for pods — so each pod only has the permissions it needs. At the network layer I use private 
subnets, VPC peering for inter-account communication, security groups with minimal open ports, 
and NACLs as a secondary control. For API security I've secured 10+ API Gateway endpoints with Lambda 
custom authorizers. We enforce TLS/SSL on all ALB listeners. Terraform enforces infrastructure standards
so no manual exceptions slip through. For the banking client we also follow BFSI compliance standards a
nd conduct regular access reviews.
Q8
Situational
How have you contributed to cloud cost optimisation?
Your answer
I led FinOps initiatives for BMO's AWS environment. First, I enforced tagging standards so every resource 
is attributable to a team and workload — without tags you can't optimise what you can't see. 
Then I right-sized EC2 instances by analysing CloudWatch utilisation metrics over 4 weeks and 
identifying over-provisioned instances. I also reviewed Reserved Instance coverage gaps and presented 
recommendations to the team. Combined, these initiatives delivered an estimated 20–25% reduction in 
monthly cloud spend. I also built auto-scaling policies on EKS node groups so we don't over-provision 
for off-peak hours.

Q9
Behavioural
Why are you looking for a new role, and why this one specifically?
Your answer
I've had a strong 4 years at TCS and I'm proud of what I've built for BMO — but I'm at a stage where
I want to own infrastructure decisions end-to-end, not just execute within a large delivery structure. 
This role appeals to me because it's focused on high-traffic, high-scale platforms where reliability
and automation are mission-critical — which is exactly the environment I've thrived in. I want to 
contribute to architecture decisions, not just operations, and grow toward a platform engineering 
or SRE leadership track.
Q10
Situational
Do you have 5 years? The JD requires 5+ years of experience.
Your answer
I have 4 years, and I want to be upfront about that. However, I've been working on Tier-1 banking 
production infrastructure from my very first year — not internal tooling, sandbox environments, 
or shadow work. I've owned incident response, architected EKS clusters, built Terraform IaC across
3 AWS accounts, and delivered FinOps outcomes for Bank of Montreal under a strict 99.9% SLA. 
The depth and production ownership I've had is comparable to what many engineers accumulate 
in 5–6 years in less critical environments. I'm confident I can hit the ground running at the senior level.
