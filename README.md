# AWS S3 Static Website 

This project demonstrates hosting a static website on **Amazon S3** and later automating deployment with **GitHub Actions**.

## Current Phase
- Phase 1: Manual deployment to S3
- Phase 2: CI/CD automation (coming soon)

## Stack
- HTML & CSS
- AWS S3
- AWS CLI
- GitHub

## Live URL
(Add the S3 website endpoint here# AWS S3 Static Website with CI/CD

This project demonstrates how to **host a static website on Amazon S3** and **automate deployments using GitHub Actions**.  
Every time you push changes to the `main` branch, the site is automatically updated — no manual uploads required. 🚀

## 🌐 Live Demo
Visit the deployed website here:  
**[http://jefferson-static-site-2025.s3-website-eu-west-1.amazonaws.com](http://jefferson-static-site-2025.s3-website-eu-west-1.amazonaws.com)**

---

## 📖 Project Overview
This project started as a simple static website manually deployed to AWS S3.  
It was later enhanced with a **CI/CD pipeline** that automatically syncs changes from GitHub to S3.

### Features:
- Static site hosted entirely on **AWS S3**
- Secure IAM user with least privilege for deployments
- **CI/CD pipeline** using GitHub Actions
- Automatic deployments triggered by `git push`
- Public bucket policy with restricted permissions

---

## 🗂 Project Structure
```aws-s3-static-site/
├── website/ # Static site files
│ ├── index.html
│ └── style.css
├── .github/
│ └── workflows/
│ └── deploy.yml # GitHub Actions workflow
├── .gitignore
└── README.md
```

> **Note:**  
> Only the contents of the `website/` folder are deployed to AWS S3.

---

## 🛠 Technologies Used
| Technology        | Purpose |
|-------------------|---------|
| **AWS S3**        | Static website hosting |
| **IAM**           | Secure permissions & credentials |
| **AWS CLI**       | Manual bucket management & deployments |
| **GitHub Actions**| Automating CI/CD pipeline |
| **HTML / CSS**    | Website content |

---

## 🚀 CI/CD Pipeline Overview
The deployment workflow is fully automated:

1. **Push changes** to the `main` branch.
2. GitHub Actions **runs the deploy workflow**:
   - Loads AWS credentials securely from GitHub Secrets.
   - Uses the AWS CLI to sync files to S3.
3. **Live website updates automatically** — no manual steps required.

### Workflow File: `.github/workflows/deploy.yml`


👤 Author:
Jefferson Arcanjo
Github: Arcanjo-jefferson
Linkedln: https://www.linkedin.com/in/jeffersonarcanjo/
