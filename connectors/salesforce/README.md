# Integrating Salesforce with Cursor Chat

This guide helps you configure **Cursor IDE** to access **Salesforce org** via **Cursor's chat interface**. By the end of this guide, you'll be able to run Salesforce queries and interact with live org data directly from Cursor chat.

## 📋 Prerequisites

Ensure you have the following before starting:

- ✅ Windows 10/11, macOS, or Linux
- ✅ Cursor IDE (Install via Company Portal/Kandji)
- ✅ Admin rights for software installation
- ✅ Access to a Salesforce org (Developer, Sandbox, or Production)

## 🧰 Step 1: Install Salesforce CLI

Salesforce CLI (`sf`) allows Cursor to communicate with your Salesforce org via authenticated sessions.

### 🪟 For Windows

1. **Install Salesforce CLI**
   - [Download the Windows installer (.msi)](https://developer.salesforce.com/tools/salesforcecli)
   - Run as Administrator and follow setup prompts

2. **Verify Installation**
   ```bash
   sf --version
   ```
   Output should be similar to: `@salesforce/cli/2.x.x`

### 🍏 For macOS

1. **Install Homebrew** (if not installed)
   ```bash
   brew --version  # Check if installed
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
   eval "$(/opt/homebrew/bin/brew shellenv)"
   ```

2. **Install Salesforce CLI & Tools**
   ```bash
   brew update
   brew install salesforce-cli
   brew install node
   ```

3. **Verify Installation**
   ```bash
   sf --version
   which sf
   ```

4. **Fix shell config or permissions if needed**
   ```bash
   echo 'export PATH="/opt/homebrew/bin:$PATH"' >> ~/.zshrc
   source ~/.zshrc
   ```

## 🧩 Step 2: Install Salesforce Extensions in Cursor

1. **Open Extensions Panel**
   - Press `Ctrl+Shift+X` (Windows/Linux) or `Cmd+Shift+X` (macOS)

2. **Install Extensions**
   Search and install:
   - **Salesforce CLI Integration**
   - **Salesforce Extension Pack**

3. **Reload Cursor**
   - `Ctrl+Shift+P` or `Cmd+Shift+P`
   - Type `Developer: Reload Window` → Enter

## 🔌 Step 3: Connect Cursor to Salesforce

This step enables Cursor's chat to run queries against your Salesforce org.

1. **Open Command Palette in Cursor**
   - `Ctrl+Shift+P` (Win/Linux) or `Cmd+Shift+P` (macOS)

2. **Authorize Salesforce Org**
   - Search: `SFDX: Authorize an Org`
   
   If unavailable, run this in the terminal:
   ```bash
   sf org login web --alias <org_alias>
   ```

3. **Choose the right login environment:**
   - **Default** → Production or Developer Org
   - **Sandbox** → Sandbox URL
   - **Custom Domain** → Enter your custom domain

4. **Complete login in browser**
   - Sign in with your Salesforce credentials
   - Grant access when prompted

5. **Set Default Org Alias** (optional but helpful)
   ```bash
   sf config set target-org <your-org-alias>
   ```

## 💬 Step 4: Use Cursor Chat to Query Salesforce Data

With authentication complete, you can now use **natural language prompts** in Cursor Chat to interact with Salesforce!

### Example Prompt:

> **💡 Try this prompt:** "Can you write and execute a simple query to check authentication with Salesforce org?"

## 🛠️ Troubleshooting

### Common Issues (All Platforms)

#### CLI Not Found
- Check `sf --version`
- Restart terminal or Cursor
- Confirm PATH is set

#### Auth Issues
- Clear browser cache
- Run `sf org logout` then re-authenticate
- Check network/firewall

#### Extensions Not Working
- Ensure all required extensions installed
- Reload window
- Check Output logs

### macOS-Specific Fixes

#### sf: Command Not Found
```bash
which sf
brew list | grep salesforce
brew uninstall salesforce-cli && brew install salesforce-cli
echo 'export PATH="/opt/homebrew/bin:$PATH"' >> ~/.zshrc && source ~/.zshrc
```

#### Permission Issues
```bash
sudo chown -R $(whoami) ~/.npm
sudo chown -R $(whoami) /opt/homebrew
sudo chown -R $(whoami) /usr/local/lib/node_modules/@salesforce
```

## 🎉 You're All Set!

You should now be able to:

- ✅ Authenticate Cursor with your Salesforce org
- ✅ Run SOQL queries using natural prompts in Cursor chat
- ✅ Interact with live Salesforce data directly from your IDE

**Happy Salesforce Development with Cursor!** 🧠 + ⚡ + ☁️

---

## Additional Resources

- [Salesforce CLI Documentation](https://developer.salesforce.com/tools/salesforcecli)
- [Cursor IDE Documentation](https://cursor.sh/docs)
- [Salesforce Developer Documentation](https://developer.salesforce.com/)

## Configuration Files

See the `config/` directory for:
- `config.example.json` - Configuration template
- `sfdx-project.json` - Salesforce project configuration

## Scripts and Templates

Explore the following directories:
- `scripts/` - Automation and utility scripts
- `templates/` - Code templates for Apex, LWC, etc.
- `examples/` - Working examples and use cases