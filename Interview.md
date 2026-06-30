1) what are the different enviroments you used in your Project

In my current banking project at TCS for the Bank of Montreal, we primarily worked with three environments: Development, Staging (or UAT), and Production. We maintained separate AWS accounts for each environment using Terraform workspaces and remote state isolation. This ensured complete separation between environments."
Development Environment:
Developers committed code to GitLab. CI/CD pipelines automatically built Docker images, executed unit tests, pushed images to the registry, and deployed them to the Development EKS cluster.
 Here we validated new features and infrastructure changes.

Staging/UAT Environment: 
After successful testing in Dev, the same Helm charts and Terraform modules were promoted to Staging. This environment closely matched Production and was used for integration testing, performance testing, security validation, and business user acceptance.

Production Environment: 
Once all approvals were completed, deployments were performed through GitLab CI/CD with controlled approvals. We used rolling updates on Amazon EKS to ensure zero downtime. Monitoring was done using Prometheus, Grafana, Dynatrace, and CloudWatch, and if any issue occurred, we had rollback mechanisms through our CI/CD pipeline."

2) how you troubleshoot application slowness.

"In my project, I first check Grafana and CloudWatch dashboards to identify whether the issue is related to infrastructure or the application. Then I verify Kubernetes pod health, CPU, memory, and logs. If the issue is caused by resource exhaustion, I scale the pods. If it started after a deployment, I roll back using the GitLab CI/CD pipeline. If infrastructure is healthy, I work with the application team to investigate slow database queries or application code. This systematic approach helps identify the root cause quickly instead of guessing

3)  statefull & stateless
   stateful : Stateful applications require persistent storage and stable identities. Kubernetes uses StatefulSets to manage them, ensuring each pod has a unique hostname and its own Persistent Volume
ex: MySQL, PostgreSQL, MongoDB
stateless :  Stateless applications do not maintain session or user data. Each request is independent, making them easy to scale and manage. In Kubernetes, we typically deploy stateless applications using Deployments
ex: Nginx, Web servers
Easy way to remember
Deployment = Stateless = No data
StatefulSet = Stateful = Data + Persistent Storage

4)   what you will do by using terraform
   In my project, I used Terraform as an Infrastructure as Code (IaC) tool to automate the provisioning and management of AWS infrastructure. Instead of creating resources manually through the AWS Console, I wrote reusable Terraform modules and stored them in Git. This allowed us to create consistent infrastructure across Development, Staging, and Production environments.
"Using Terraform, I provisioned:

    1 ) VPCs, subnets, route tables, Internet and NAT Gateways
    2) Security Groups and IAM roles
    3) EC2 instances
    4) Amazon EKS clusters
    5) Application Load Balancers
    6) S3 buckets for remote state
    7) RDS databases
    8) Auto Scaling resources and CloudWatch alarms"
    workflow was:

Write Terraform code.
    1) Store it in GitLab.
    2) Run terraform fmt and terraform validate.
    3) Execute terraform plan to review changes.
    4) After approval, run terraform apply through the GitLab CI/CD pipeline.
    5) Terraform stored the state file in an S3 bucket with state locking to prevent concurrent modifications."

5) what is PV &  pvc

PV :  A Persistent Volume (PV) is the actual storage available in the Kubernetes cluster. It can come from:
AWS EBS &Local storage

Think of it as a hard disk provided to Kubernetes.

What is PVC (Persistent Volume Claim)?
iT is a request for storage made by a pod,Instead of directly using a PV, a pod requests storage through a PVC.
Kubernetes automatically binds the PVC to a matching PV.

    Easy analogy
  Imagine you're staying in a hotel:
  Hotel Room = Persistent Volume (PV)
  Room Booking = Persistent Volume Claim (PVC)
  Guest = Pod
 


