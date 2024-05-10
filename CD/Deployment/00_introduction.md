# 🚀 Continuous Delivery on AWS

This project demonstrates how to implement a **Continuous Delivery (CD) pipeline fully on AWS** using **PaaS and SaaS services only**.
No EC2 instances are managed directly, resulting in **minimal operational overhead** and a **developer-friendly delivery model**.

### ❓ Why Continuous Delivery on AWS?

#### Problem Scenario

Modern product teams typically operate in **Agile environments**, where:

- Developers make **frequent code changes**
- Every change must be:

  - Built
  - Tested
  - Deployed
  - Validated again (integration & functional tests)

- Teams often have:

  - Few or no dedicated operations engineers
  - Developers and testers without deep ops expertise

Manual or ops-heavy deployments:

- Slow down delivery
- Increase dependency on ops teams
- Increase risk and MTTR (Mean Time To Repair)

### ⚠️ Challenges with Traditional Approaches

- CI/CD tools (Jenkins, Nexus, SonarQube) require:

  - EC2 instances
  - Continuous maintenance and patching

- Target environments (VMs / EC2):

  - Need constant management
  - Increase operational complexity

- Release ownership is tightly coupled with operations teams

This model is inefficient—especially for **pre-prod, QA, and test environments**.

### ✅ Solution: Cloud-Based Continuous Delivery

By leveraging **AWS managed services**, teams can:

- Eliminate server management
- Reduce reliance on ops teams
- Enable developers and testers to deploy independently
- Create **disposable and reproducible environments**
- Fully automate build, test, deploy, and validation stages

#### Benefits

- Faster feedback cycles
- Lower MTTR
- Minimal human intervention
- Cloud-native scalability

### 🎯 Key Objectives of This Project

- Zero or near-zero operations overhead
- Fully automated CI/CD pipeline
- Fast feedback on every code change
- Quick bug isolation and recovery
- Cloud-native, scalable delivery model

### 🧰 AWS Services Used

#### Source & CI/CD

- **AWS CodeCommit** – Source control
- **AWS CodeArtifact** – Maven dependency management
- **AWS CodeBuild** – Build, test, code analysis, Selenium tests
- **AWS CodePipeline** – Pipeline orchestration

#### Code Quality & Testing

- **SonarCloud** – Static code analysis
- **Checkstyle** – Code style validation
- **Selenium** – Automated functional testing

#### Deployment & Runtime

- **AWS Elastic Beanstalk** – Application hosting (no EC2 management)
- **Amazon RDS** – Managed database service
- **Amazon S3** – Artifact and test report storage

### 🔄 CI vs CD: What Changes in This Project?

#### Reused from the CI Project

- SonarCloud code analysis
- Dependency management via CodeArtifact
- Artifact build job
- S3 artifact storage
- CodePipeline orchestration

#### Newly Added for Continuous Delivery

- Deployment to **Elastic Beanstalk**
- **Amazon RDS** integration
- Selenium-based post-deployment testing
- Automated validation after deployment

### 🏗️ Continuous Delivery Pipeline Architecture

#### High-Level Flow

1. Developer commits code to **CodeCommit**
2. Pipeline triggers automatically
3. **CodeBuild**:

   - Runs unit tests
   - Performs SonarCloud analysis
   - Pulls dependencies from CodeArtifact

4. Artifact is built and stored in **S3**
5. Artifact is deployed to **Elastic Beanstalk**
6. Application connects to **Amazon RDS**
7. Selenium tests run against the Beanstalk environment
8. Test reports are stored in **S3**
9. Pipeline completes with full delivery automation

### 🔁 Traditional vs AWS-Managed Approach

| Traditional Tool / Platform | AWS Managed Service |
| --------------------------- | ------------------- |
| GitHub                      | AWS CodeCommit      |
| Nexus Repository            | AWS CodeArtifact    |
| Jenkins Jobs                | AWS CodeBuild       |
| Jenkins Pipeline            | AWS CodePipeline    |
| SonarQube Server            | SonarCloud          |
| Tomcat on EC2               | Elastic Beanstalk   |
| Database on VM / EC2        | Amazon RDS          |

**Result**

- ✔ No server management
- ✔ Lower operational cost
- ✔ Faster delivery cycles
- ✔ Reduced dependency on ops teams
