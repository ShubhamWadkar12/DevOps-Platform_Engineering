# 🔄 CI/CD

CI/CD is one of the core practices of DevOps that helps teams build, test, and deploy software quickly and reliably.

Instead of manually building, testing, and deploying applications, CI/CD automates these processes. This reduces human errors, speeds up software delivery, and ensures high-quality releases.

Today, almost every modern software company uses CI/CD pipelines to deliver software continuously.

---

# 🎯 Learning Objectives

After completing this topic, you will be able to:

* Understand what CI and CD mean.
* Learn the difference between Continuous Delivery and Continuous Deployment.
* Understand how a CI/CD pipeline works.
* Learn the benefits of CI/CD.
* Become familiar with popular CI/CD tools.

---

# 📌 What is CI/CD?

**CI/CD** stands for:

* **CI** – Continuous Integration
* **CD** – Continuous Delivery or Continuous Deployment

It is a DevOps practice that automates the process of integrating code changes, testing applications, and deploying software.

---

# 📌 What is Continuous Integration (CI)?

**Continuous Integration (CI)** is the practice of regularly merging code changes into a shared repository.

Whenever a developer pushes code, an automated pipeline:

* Builds the application.
* Runs automated tests.
* Detects errors early.
* Reports the build status.

This helps teams identify and fix issues before they become larger problems.

---

# 📌 What is Continuous Delivery (CD)?

**Continuous Delivery** automatically prepares software for release after successful testing.

The application is ready to deploy at any time, but a **manual approval** is required before it is released to production.

---

# 📌 What is Continuous Deployment?

**Continuous Deployment** automatically deploys every successful code change to production without manual approval.

As soon as all automated tests pass, the new version is released to users.

---

# 📊 Continuous Delivery vs Continuous Deployment

| Continuous Delivery               | Continuous Deployment                      |
| --------------------------------- | ------------------------------------------ |
| Manual approval before production | No manual approval required                |
| Release is controlled by the team | Release happens automatically              |
| Lower deployment risk             | Faster delivery to users                   |
| Common in enterprise applications | Common in modern cloud-native applications |

---

# 🔄 CI/CD Pipeline

```text
Developer Writes Code
          ↓
Push Code to Git Repository
          ↓
CI Pipeline Starts
          ↓
Build Application
          ↓
Run Automated Tests
          ↓
Generate Build Artifact
          ↓
CD Pipeline
          ↓
Deploy to Staging
          ↓
Manual Approval (Continuous Delivery)
          ↓
Deploy to Production
```

---

# 🛠️ Popular CI/CD Tools

| Tool                   | Purpose                                  |
| ---------------------- | ---------------------------------------- |
| Jenkins                | Build and Deployment Automation          |
| GitHub Actions         | CI/CD Automation for GitHub repositories |
| GitLab CI/CD           | Integrated CI/CD for GitLab              |
| Azure DevOps Pipelines | Build and Release Automation             |
| CircleCI               | Cloud-based CI/CD Platform               |
| Argo CD                | Continuous Deployment for Kubernetes     |

---

# 🌍 Real-World Example

Imagine a developer fixes a bug in an **Online Shopping Application**.

1. The developer pushes the code to GitHub.
2. GitHub Actions automatically starts the CI pipeline.
3. The application is built.
4. Automated tests are executed.
5. If all tests pass, the application is deployed to the staging environment.
6. After approval, the application is deployed to production.

The entire process is automated, reducing manual work and improving reliability.

---

# 🛠️ Hands-on

* Create a GitHub repository.
* Add a simple application.
* Create a basic GitHub Actions workflow.
* Automatically build the project when code is pushed.
* Observe the workflow execution in the **Actions** tab.

---

# ✅ Benefits

* Faster software delivery.
* Early bug detection.
* Improved software quality.
* Reduced manual effort.
* Consistent deployments.
* Faster feedback for developers.
* Reliable release process.

---

# ⚠️ Limitations

* Initial setup can take time.
* Automated pipelines require maintenance.
* Poorly designed tests can reduce pipeline effectiveness.
* Infrastructure costs may increase for large projects.

---

# 💼 Interview Questions

* **What is CI/CD?**                                
  CI/CD is a DevOps practice that automates building, testing, and deploying software.

* **What does CI stand for?**                                      
  CI stands for **Continuous Integration**, where developers frequently merge code changes into a shared repository.

* **What does CD stand for?**                                          
  CD stands for **Continuous Delivery** or **Continuous Deployment**.

* **What is the difference between Continuous Delivery and Continuous Deployment?**                                     
  Continuous Delivery requires manual approval before production, while Continuous Deployment automatically deploys every successful change to production.

* **Why is Continuous Integration important?**                               
  It detects errors early, improves code quality, and helps developers integrate changes frequently.

* **What is a CI/CD pipeline?**                          
  A CI/CD pipeline is an automated workflow that builds, tests, and deploys applications.

* **Name some popular CI/CD tools.**                                
  Jenkins, GitHub Actions, GitLab CI/CD, Azure DevOps Pipelines, CircleCI, and Argo CD.

---

# 📚 Navigation

⬅️ Previous: **[09-DevOps Lifecycle](09-DevOps-Lifecycle.md)**

➡️ Next: **[11-Modern DevOps](11-Modern-DevOps.md)**
