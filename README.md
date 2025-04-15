# 📦 React Static Website Deployment on AWS with CI/CD


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

- Enable static website hosting
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
  }


### 4. Uploaded the React build to S3 manually

- Used the `/client/build` folder contents (Upload build folder content not whole build folder)

### 5. Set up CloudFront (Create Distribution)

- Origin: S3 website endpoint
- Add default root object index.html
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

![CI/CD Architecture](https://cdn.hashnode.com/res/hashnode/image/upload/v1744715062055/69038515-e215-4c40-aa65-8dd247718022.jpeg?w=1600&h=840&fit=crop&crop=entropy&auto=compress,format&format=webp)

---

### InShort 

1. Clone repo → cd project_chat_application → cd client → npm install → npm run build
2. Setup s3 bucket → enable static website hosting → add bucket policy → upload build content → `project_chat_app/client/build` → (upload build folder content not whole build folder)
3. Create CloudFront Distribution →
4. CI/CD with Codepipeline + Codebuild → Create Pipeline → & add Build Stage
5. Test it: Open the CloudFront domain or your custom domain.
