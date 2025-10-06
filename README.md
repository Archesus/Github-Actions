# 🚀 AWS S3 Static Website Deployment with GitHub Actions

This repository demonstrates how to automatically deploy a **static website** to an **Amazon S3 bucket** using **GitHub Actions**.  
Whenever you push changes to the `main` branch, the workflow builds and uploads your website files to S3 — fully automated! 🌐

---

## 🧩 Features

- 🧱 Static website hosted on **Amazon S3**
- ⚙️ **Continuous Deployment** with GitHub Actions
- 🔒 Secure access using AWS credentials stored in GitHub Secrets
- 📦 Automatic sync — only changed files are updated
- 🚀 Zero manual intervention after setup

---

## 🏗️ Project Structure

📁 project-root/
├── 📂 .github/
│   └── 📂 workflows/
│       └── 🧩 deploy.yml            # GitHub Actions workflow for S3 deployment
│
├── 🏠 index.html                    # Main website file (entry point)
├── 📂 assets/                       # Static assets (CSS, JS, images)
│   ├── styles.css
│   ├── script.js
│   └── images/
│
└── 📝 README.md                     # Project documentation


---

## ⚙️ How It Works

1. You push changes to the `main` branch.
2. GitHub Actions triggers the `deploy.yml` workflow.
3. The workflow:
   - Installs dependencies (if any)
   - Builds your static website (optional step)
   - Deploys files to the specified S3 bucket
4. Your site goes live instantly on S3! 🎉

---

## 🔐 Required GitHub Secrets

Before running the workflow, make sure to set these secrets in  
**Repository Settings → Secrets → Actions**:

| Name | Description |
|------|--------------|
| `AWS_ACCESS_KEY_ID` | Your AWS access key |
| `AWS_SECRET_ACCESS_KEY` | Your AWS secret key |
| `AWS_REGION` | AWS region (e.g., `ap-south-1`) |
| `S3_BUCKET` | Name of your S3 bucket |

---

## 📝 Example GitHub Actions Workflow

```yaml
name: Deploy Static Website to S3

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout source
        uses: actions/checkout@v4

      - name: Sync files to S3
        uses: jakejarvis/s3-sync-action@master
        with:
          args: --delete
        env:
          AWS_S3_BUCKET: ${{ secrets.S3_BUCKET }}
          AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
          AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          AWS_REGION: ${{ secrets.AWS_REGION }}
          SOURCE_DIR: './'
```

## 🌍 Accessing the Website

Once deployed, your static website can be accessed via your S3 public endpoint, such as:

http://<your-bucket-name>.s3-website-<region>.amazonaws.com


You can also configure a custom domain and SSL certificate using AWS CloudFront for added performance and security.

## 🧠 Useful Commands
# Initialize git
git init

# Add remote
git remote add origin https://github.com/<your-username>/<your-repo>.git

# Push changes
git add .
git commit -m "Initial commit"
git push -u origin main

## 🏁 Conclusion

This setup provides a simple, serverless, and cost-effective way to deploy and manage your static websites using AWS S3 + GitHub Actions.
You get continuous delivery, version control, and automated deployment — all in one workflow!

💙 Author

Anurag Kumar

Frontend Developer • UI/UX Designer • Cloud Enthusiast
