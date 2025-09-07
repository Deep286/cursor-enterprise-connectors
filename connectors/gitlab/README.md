# Integrating GitLab with Cursor Chat

This guide walks you through integrating **GitLab** with **Cursor IDE** for efficient development workflows and repository management using natural language prompts.

## ✅ Prerequisites

Ensure the following before proceeding:

- 💻 Cursor IDE installed and functional
- 🔐 Access to your organization's GitLab instance
- 🧾 A valid GitLab account with API access permissions
- ⚙️ Git installed on your system

## 📦 Step 1: Install Required Tools

### 🔧 Install Git

- Use **Company Portal** (Windows) or **Kandji** (macOS) to install Git.
- **Verify Git Installation**: Open your terminal or PowerShell and run:
  ```bash
  git --version
  ```

- **Set your global Git identity** to align with your GitLab account:
  ```bash
  git config --global user.name "FIRST_NAME LAST_NAME"
  git config --global user.email "your.name@your-company.com" 
  git config --global core.longpaths true
  ```

## 🔐 Step 2: Configure GitLab API Access

### 1. **Create a GitLab Personal Access Token**

1. Go to: **GitLab Settings** → **Personal Access Tokens**
   - For GitLab.com: [https://gitlab.com/-/profile/personal_access_tokens](https://gitlab.com/-/profile/personal_access_tokens)
   - For self-hosted: `https://your-gitlab.com/-/profile/personal_access_tokens`

2. Click **Add new token**

3. Fill in the details:
   - **Name**: `Cursor-Development`
   - **Expiration**: (Recommended: 1 year)
   - **Scopes**:
     - ✅ `api` (full API access)
     - ✅ `read_api` (read API access)
     - ✅ `read_repository` (read repository)

4. Click **Create personal access token**
5. **Copy the token immediately** – it will not be shown again!

### 2. **Create the `.gitlab_config` File**

| OS | File Path |
|---|---|
| Windows | `C:\Users\{your-username}\.gitlab_config` |
| macOS/Linux | `~/.gitlab_config` |

### 3. **Add Your Configuration**

```bash
# GitLab API Configuration
export GITLAB_URL="https://gitlab.com"  # or your self-hosted URL
export GITLAB_TOKEN="your-actual-token-here"
```

## 💬 Cursor Chat Example Prompt

Once setup is complete, test GitLab access in Cursor chat:

> **💡 Try this prompt:** "Load credentials from ~/.gitlab_config and authenticate"

## 🎯 What You Can Do Now

- **Repository Management**: Create, clone, and manage repositories
- **CI/CD Integration**: Monitor pipelines and trigger deployments
- **Issue Tracking**: Create and manage issues with natural language
- **Merge Requests**: Automate MR workflows and code reviews

## 🛠️ Troubleshooting

| Issue | Fix |
|---|---|
| Config file not found | Ensure correct path and filename |
| Authentication failed | Check token and GitLab URL |
| Permission denied | Verify token scopes |

## 🎉 You're All Set!

**Happy GitLab Integration with Cursor!** 🧠 + 🦊 + 🚀

---

For detailed usage examples and advanced configuration, see the `examples/` and `scripts/` directories.