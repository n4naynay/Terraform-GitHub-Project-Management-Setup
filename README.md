# 🚀 GitHub Repository Management with Terraform

This project uses **Terraform** to automate GitHub repository operations, including:

- Repository creation
- Collaborator management
- Dynamic GitHub Actions secrets (repo and org level)
- Webhook integration
- Optional branch creation and protection rules

It also includes a CI/CD pipeline powered by **GitHub Actions**.

---

## 🌟 Features

- ✅ Create and initialize GitHub repositories
- ✅ Add collaborators with specific permissions
- ✅ Dynamically inject GitHub Actions secrets (repo-level or org-level)
- ✅ Configure GitHub Webhooks (URL, content type, SSL, secret)
- ✅ Create feature branches (`develop`, `staging`, `release`)
- ✅ Built-in CI pipeline: `fmt`, `validate`, `plan`, manual `apply`
- ✅ Support for reusable and modular Terraform design

---

## ⚙️ Requirements

- [Terraform ≥ 1.4](https://www.terraform.io/downloads.html)
- [jq](https://stedolan.github.io/jq/) installed  
  → `sudo apt install jq` or `brew install jq`
- GitHub Personal Access Token (PAT) with:
  - `repo`
  - `admin:repo_hook`
  - `admin:org` (for org-level secrets)

---

## 🔐 Environment Setup

### 1. Create a `.env` file

```bash
# GitHub Settings
GITHUB_TOKEN="ghp_..."
GITHUB_OWNER="Blue-Lambda-University"
COLLABORATORS='["bluelambdatech", "nene", "omolewa"]'

# Repo-level secrets
SECRETS='{
  "MY_SECRET": "supersecretvalue",
  "EC2_HOST": "your.ec2.host",
  "EC2_SSH_KEY": "<private-key>",
  "EC2_USER": "ubuntu"
}'

# Org-level secrets (optional)
ORG_SECRETS='{
  "ORG_API_TOKEN": "org-token",
  "ORG_ENDPOINT": "https://org.example.com"
}'

# Webhook Configuration
WEBHOOK_URL="http://your-jenkins-url/github-webhook/"
WEBHOOK_SECRET="webhook-secret-token"
WEBHOOK_CONTENT_TYPE="application/x-www-form-urlencoded"
INSECURE_SSL=false
```

### 2. Run with Script
```bash
chmod +x load-env.sh
./load-env.sh
```

This loads variables, exports them as `TF_VAR_*`, and applies Terraform.

> You can also trigger `plan` and `apply` through GitHub Actions.

---

## 🤖 GitHub Actions Workflow
The CI/CD pipeline defined in `.github/workflows/terraform.yml`:
- Runs on push or PR to `main`
- Caches plugins
- Performs `terraform fmt`, `validate`, and `plan`
- Uploads the plan artifact
- (Optional) Deploys via manual approval on push to main

---

## 🔐 Security
- `.env` is listed in `.gitignore`
- Secrets like EC2 credentials and GitHub tokens are stored securely via `github_actions_secret`
---

## 🧼 Clean Up
```bash
terraform destroy
```

---

## 📎 License
MIT © Blue Lambda Technologies

---

Need help? Contact [info@bluelambdatechnologies.com](mailto:info@bluelambdatechnologies.com)
