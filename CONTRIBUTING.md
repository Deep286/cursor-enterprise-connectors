# Contributing to Cursor Enterprise Connectors

Thank you for your interest in contributing! This project provides simple integration guides for connecting Cursor IDE with enterprise platforms.

## 🤝 How to Contribute

### Reporting Issues

1. **Search existing issues** first to avoid duplicates
2. **Provide clear details**:
   - Which platform (Salesforce, Atlassian, GitLab, Boomi, TestRail)
   - Steps you followed
   - What worked vs. what didn't
   - Your environment (OS, Cursor version)

### Suggesting Improvements

1. **Open an issue** describing the improvement
2. **Explain the use case** and how it helps users
3. **Provide examples** if possible

### Contributing Content

#### Setup Instructions
1. **Fork the repository**
2. **Clone your fork**:
   ```bash
   git clone https://github.com/your-username/cursor-enterprise-connectors.git
   cd cursor-enterprise-connectors
   ```
3. **Create a branch**: `git checkout -b improve-salesforce-guide`

#### Making Changes
- **Update integration guides** with clearer instructions
- **Add missing troubleshooting steps**
- **Improve configuration examples**
- **Fix broken links or outdated information**

#### Testing Your Changes
- **Test the integration steps** yourself if possible
- **Verify all links work**
- **Check that configuration examples are correct**
- **Ensure screenshots/examples are current**

## 📝 Content Guidelines

### Integration Guides
- Use **clear, step-by-step instructions**
- Include **real working examples** (with placeholders for sensitive data)
- Add **troubleshooting sections** for common issues
- Provide **example Cursor prompts** that users can try

### Configuration Files
- Always use **placeholder values** (never real credentials)
- Follow the **existing format** for consistency
- Include **comments** explaining each field
- Test that the **structure is valid JSON**

### Documentation Style
- Write in **clear, simple language**
- Use **bullet points** for steps
- Include **code blocks** for commands
- Add **warnings** for security-sensitive steps

## 🔐 Security Guidelines

### Never Include:
- Real API tokens or credentials
- Company-specific URLs or identifiers
- Personal information

### Always Include:
- Placeholder values (e.g., `your-api-token-here`)
- Security warnings about credential handling
- References to secure storage practices

## 🚀 Adding New Platforms

To add support for a new platform:

1. **Create directory**: `connectors/[platform-name]/`
2. **Add README.md** following existing format:
   - Prerequisites
   - Step-by-step setup
   - Configuration examples
   - Example Cursor prompts
   - Troubleshooting
3. **Create config template**: `connectors/[platform-name]/config/config.example.json`
4. **Update main README** to include the new platform

## ✅ Pull Request Checklist

Before submitting:
- [ ] Tested the integration steps personally
- [ ] Used placeholder values (no real credentials)
- [ ] Updated relevant documentation
- [ ] Followed existing formatting style
- [ ] Added troubleshooting for common issues

## 🎯 What We're Looking For

- **Clearer setup instructions**
- **Better troubleshooting guides**
- **More platform integrations**
- **Improved configuration examples**
- **Documentation fixes**

## ❓ Questions?

Open an issue if you have questions about contributing. We're here to help!

---

Thank you for helping make enterprise integrations easier for everyone! 🙏