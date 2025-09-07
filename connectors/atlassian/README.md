# Integrating Atlassian with Cursor Chat

This guide walks you through the steps to integrate **Atlassian Jira & Confluence** with **Cursor IDE**, enabling seamless ticket management and documentation workflows using natural language prompts in Cursor Chat.

## ✅ Prerequisites

Ensure you have the following before starting:

- 🧠 Cursor IDE installed and running
- 🔑 Access to your organization's Jira instance (e.g., `https://your-company.atlassian.net`)
- 🧾 Valid Jira account with API token permissions
- 💻 Access to PowerShell (Windows) or Terminal (macOS/Linux)

## 🔐 Step 1: Create Your Jira API Token

To allow Cursor IDE to authenticate and interact with Jira securely:

1. **Go to Atlassian API Tokens Page**
   [https://id.atlassian.com/manage-profile/security/api-tokens](https://id.atlassian.com/manage-profile/security/api-tokens)

2. **Log In with Your Company Credentials**

3. **Create a Token**
   - Click **Create API Token**
   - Add a label like: `Cursor-Development`
   - Click **Create**
   - **Copy the token immediately** – it's only shown once!

## ⚙️ Step 2: Create Jira API Configuration File

Cursor will load your Jira credentials from a local config file.

### 📁 1. Create `.atlassian_config` File

| OS | File Path |
|---|---|
| Windows | `C:\Users\{your-username}\.atlassian_config` |
| macOS/Linux | `~/.atlassian_config` |

### 🧾 2. Add the Following Configuration

Replace the placeholders with your **company email** and the **API token** you just created:

```bash
export JIRA_BASE_URL="https://your-company.atlassian.net"
export CONFLUENCE_URL="https://your-company.atlassian.net/wiki"
export JIRA_EMAIL="your.email@your-company.com"
export JIRA_API_TOKEN="your-api-token-here"
```

🔒 **Keep this file private** – do not commit it to version control.

## 💬 Cursor Chat Example Prompt

After creating the config file, test it with a simple natural language prompt in Cursor chat:

> **💡 Try this prompt:** "Load credentials from C:\Users\{username}\.atlassian_config and authenticate"

Cursor should respond by confirming that the Jira credentials have been loaded successfully.

## 🎯 What You Can Do Now

With the integration set up, you can use natural language prompts to:

### 🎫 Jira Integration
- **Create Issues**: "Create a bug ticket for the login authentication error"
- **Query Issues**: "Show me all open tickets assigned to me"
- **Update Status**: "Move ticket ABC-123 to In Progress"
- **Add Comments**: "Add comment to ticket XYZ-456 about the progress update"

### 📄 Confluence Integration
- **Create Pages**: "Create a new Confluence page for API documentation"
- **Search Content**: "Find all pages related to authentication"
- **Update Documentation**: "Update the deployment guide with new steps"

### 🔄 Workflow Automation
- **Link Commits**: Automatically link code commits to Jira issues
- **Status Updates**: Update ticket status based on code changes
- **Auto-documentation**: Generate documentation from code comments

## 🛠️ Troubleshooting

| Issue | Fix |
|---|---|
| Cursor can't find config file | Ensure file is saved in the correct path and has correct file name |
| Auth failed | Double-check email/token in the file |
| Token expired | Re-generate token in Atlassian and update the config |
| Mac/Linux `export` not working | Run `source ~/.atlassian_config` to reload environment |

### Advanced Troubleshooting

#### Permission Issues
- Ensure your API token has the necessary permissions
- Check if your account has access to the projects you're trying to query

#### Network Issues
- Verify your organization's firewall allows access to Atlassian APIs
- Check if you're behind a corporate proxy

#### Configuration Issues
```bash
# Test your configuration (Linux/macOS)
source ~/.atlassian_config
echo $JIRA_BASE_URL
echo $JIRA_EMAIL

# Verify API access
curl -u "$JIRA_EMAIL:$JIRA_API_TOKEN" "$JIRA_BASE_URL/rest/api/2/myself"
```

## 🎉 You're All Set!

You've successfully connected Cursor IDE with Jira and Confluence. You can now:

- ✅ Manage tickets using conversational prompts
- ✅ Query Jira data with natural language
- ✅ Automate workflows between code and tickets
- ✅ Create and update Confluence documentation

**Happy Atlassian Integration with Cursor!** 🧠 + 🎫 + 📄

---

## Additional Resources

- [Jira REST API Documentation](https://developer.atlassian.com/cloud/jira/platform/rest/)
- [Confluence REST API Documentation](https://developer.atlassian.com/cloud/confluence/rest/)
- [Atlassian API Tokens Guide](https://support.atlassian.com/atlassian-account/docs/manage-api-tokens-for-your-atlassian-account/)

## Configuration Files

See the `config/` directory for:
- `config.example.json` - Configuration template
- `jira-fields.json` - Jira field mappings
- `workflows.json` - Custom workflow definitions

## Scripts and Examples

Explore the following directories:
- `scripts/` - Jira automation scripts
- `templates/` - Issue and page templates  
- `examples/` - Integration workflows and use cases