# 📦 React Static Website Deployment on AWS with CI/CD

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
---



## ⚙️ Setup Instructions

### 1. Clone the Repo

```bash
git clone https://github.com/VisheshGhule/project_chat_application.git
cd project-chat-application/client
```

### 2. Install dependencies and build

> ⚠️ Make sure you're inside the `client/` folder before running these commands.

 ```bash
npm install
npm run build
```

### 3. Created an S3 bucket on AWS

- Enabled static website hosting
- Set `index.html` as the default
- Add a bucket policy to allow public read access
  ```json
  {
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::my-react-app-chat/*"
    }
  ]
  }```



### 4. Uploaded the React build to S3 manually

- Used the `/client/build` folder contents (Upload build folder content not whole build folder)

### 5. Set up CloudFront

- Origin: S3 website endpoint
- Add default root object index.html
- Add HTTPS using AWS ACM
- (Optional) Linked Route 53 for a custom domain

### 6. Add a `buildspec.yml` file at the root of the repo (Already added no need to add, add when there is no builspec.yml file added)
```yml
version: 0.2

env:
  variables:
    NODE_OPTIONS: --openssl-legacy-provider

phases:
  install:
    commands:
      - cd client
      - npm install
  build:
    commands:
      - npm run build
  post_build:
    commands:
      - aws s3 sync build/ s3://my-react-app-chat --delete

artifacts:
  files:
    - '**/*'
```

### 7. Set up CodePipeline

- Source: GitHub
- Build: CodeBuild using buildspec.yml
- Deploy: S3 bucket created in step 3

### 8. Test the pipeline

- Pushed code to GitHub
- CodePipeline triggered automatically
- Site deployed to S3 and served via CloudFront 
- Open the CloudFront domain or your custom domain 🚀

### CI/CD Architecture

GitHub → CodePipeline → CodeBuild → S3 → CloudFront (with HTTPS)
