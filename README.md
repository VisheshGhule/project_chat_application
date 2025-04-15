# 📦 React Static Website Deployment on AWS with CI/CD

### 🔴 [Live Blog Walkthrough](https://visheshblog.hashnode.dev/project-1-deploying-a-static-react-website-on-aws-with-cicd-s3-cloudfront-codepipeline)

### 🚀 Hosted With: AWS S3 + CloudFront + CodePipeline  
### 🧠 Project Type: Static React Website with CI/CD from GitHub

---

## 🧠 Introduction

This is the complete code repository for my project where I hosted a **React application** on **AWS** with a fully automated deployment pipeline using **CodePipeline**, **CodeBuild**, and **S3**, served globally via **CloudFront** with HTTPS enabled.

I’ve documented everything in detail in my Hashnode blog, including all errors and learnings — perfect for beginners exploring AWS and CI/CD for the first time.

🔗 [Read the full guide](https://visheshblog.hashnode.dev/project-1-deploying-a-static-react-website-on-aws-with-cicd-s3-cloudfront-codepipeline)

---

## 🛠️ Tech Stack

**Frontend**:  
- React.js

**CI/CD**:  
- AWS CodePipeline  
- AWS CodeBuild  
- GitHub (as source provider)

**Deployment**:  
- AWS S3 (for static hosting)  
- AWS CloudFront (as global CDN)  
- AWS Certificate Manager (for HTTPS)  
- (Optional) Route 53 or custom DNS

---


---

## ⚙️ Setup Instructions

> ⚠️ Make sure you're inside the `client/` folder before running these commands.

### 1. Clone the Repo

```bash
git clone https://github.com/yourusername/project-chat-application.git
cd project-chat-application/client
