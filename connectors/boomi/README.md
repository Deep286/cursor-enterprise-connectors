# Boomi Cursor Integration

Integration guide for connecting Cursor IDE with Dell Boomi AtomSphere integration platform for enhanced process development, connector configuration, and integration workflow automation.

## ✨ Features

- **Process Development Assistance**: AI-powered help for building Boomi processes
- **Connector Configuration**: Automated setup and configuration of Boomi connectors
- **Data Mapping Support**: Intelligent data mapping and transformation assistance
- **Boomi API Integration**: Full access to AtomSphere and Platform APIs
- **Integration Testing**: Automated testing framework for Boomi integrations
- **Process Monitoring**: Real-time monitoring and alerting for running processes
- **Component Library Management**: Manage custom and reusable components

## 📋 Prerequisites

- Cursor IDE installed
- Dell Boomi AtomSphere account with appropriate permissions
- Boomi API token or OAuth credentials
- Local Boomi Atom (for testing) or access to Cloud/Molecule
- Node.js 18+ or Python 3.8+

## 🚀 Quick Start

### 1. Generate Boomi API Token

#### Using AtomSphere Interface
1. Log into Dell Boomi AtomSphere
2. Navigate to **Manage** → **Account Information and Setup**
3. Go to **API Management**
4. Create new API Token with required permissions:
   - Process Management
   - Component Access
   - Execution Management
   - Environment Access

#### Required Permissions
- `ProcessManagement:READ`
- `ProcessManagement:WRITE` 
- `ProcessManagement:EXECUTE`
- `ComponentLibrary:READ`
- `ComponentLibrary:WRITE`
- `EnvironmentManagement:READ`

### 2. Configure Authentication

```bash
# Copy configuration template
cp config/config.example.json config/config.json
```

Edit `config/config.json`:

```json
{
  "boomi": {
    "baseUrl": "https://api.boomi.com/api/rest/v1",
    "accountId": "your-account-id",
    "username": "your-username@your-company.com",
    "apiToken": "YOUR_API_TOKEN",
    "defaultEnvironment": "Test",
    "atomName": "your-local-atom",
    "oauth": {
      "clientId": "YOUR_CLIENT_ID",
      "clientSecret": "YOUR_CLIENT_SECRET",
      "tokenUrl": "https://platform.boomi.com/oauth2/token"
    }
  }
}
```

### 3. Install Dependencies

```bash
# Using npm
npm install axios xml2js form-data

# Using pip (for Python)
pip install requests python-decouple xmltodict
```

### 4. Test Connection

```bash
# Test Boomi API connection
node scripts/test_connection.js

# Test specific environment
python scripts/test_connection.py --environment "Test"
```

## 📖 Usage Examples

### Process Development

#### Generate Process Template

```
🤖 Cursor Prompt: "Create a Boomi process template for syncing Salesforce accounts to a database"
```

Expected process components:
- Salesforce Connector (Source)
- Data Process Shape (Transformation)
- Database Connector (Destination)
- Error handling and logging

#### AI-Assisted Data Mapping

```
🤖 Cursor Prompt: "Create data mapping between Salesforce Account object and MySQL customer table"
```

Generated mapping profile:
```xml
<mappingProfile>
  <field source="Name" destination="customer_name" />
  <field source="BillingAddress" destination="address" />
  <field source="Phone" destination="phone_number" />
</mappingProfile>
```

### Connector Configuration

#### Database Connector Setup

```javascript
// Auto-configure database connector
const dbConnector = {
  connectorType: "database",
  connectionProfile: {
    host: "localhost",
    port: 5432,
    database: "production",
    username: process.env.DB_USERNAME,
    password: process.env.DB_PASSWORD,
    driverType: "postgresql"
  }
};
```

#### REST API Connector

```javascript
// Configure REST API connector
const apiConnector = {
  connectorType: "http",
  baseUrl: "https://api.example.com/v1",
  authentication: {
    type: "oauth2",
    clientId: "client_id",
    clientSecret: "client_secret",
    tokenUrl: "https://api.example.com/oauth/token"
  }
};
```

### Process Monitoring

#### Real-time Process Status

```javascript
// Monitor process executions
const monitorProcess = async (processId) => {
  const executions = await boomiApi.getProcessExecutions(processId);
  
  executions.forEach(execution => {
    if (execution.status === 'ERROR') {
      console.error(`Process execution ${execution.executionId} failed`);
      notifyTeam(execution.errorDetails);
    }
  });
};
```

## 🛠️ Available Scripts

| Script | Description |
|--------|-------------|
| `scripts/process/create_process.js` | Create new Boomi processes |
| `scripts/process/deploy_process.js` | Deploy processes to environments |
| `scripts/connectors/configure.js` | Configure connector profiles |
| `scripts/mapping/generate.js` | Generate data mapping profiles |
| `scripts/testing/execute_test.js` | Execute process tests |
| `scripts/monitoring/check_status.js` | Monitor process executions |
| `scripts/components/export.js` | Export custom components |
| `scripts/environments/sync.js` | Sync between environments |

## 📁 Project Structure

```
boomi/
├── README.md
├── config/
│   ├── config.example.json     # Configuration template
│   ├── process-templates/      # Process templates
│   └── connector-profiles/     # Connector configurations
├── extension/
│   ├── extension.js            # Cursor extension entry point
│   └── commands/               # Custom commands
├── scripts/
│   ├── process/                # Process management
│   ├── connectors/             # Connector configuration
│   ├── mapping/                # Data mapping utilities
│   ├── testing/                # Testing frameworks
│   ├── monitoring/             # Process monitoring
│   └── deployment/             # Deployment automation
├── templates/
│   ├── processes/              # Process templates
│   ├── mappings/               # Mapping templates
│   └── connectors/             # Connector templates
├── examples/
│   ├── basic-integration/      # Simple integration examples
│   ├── complex-workflows/      # Advanced workflow examples
│   └── error-handling/         # Error handling patterns
└── tests/
    ├── unit/                   # Unit tests
    └── integration/            # Integration tests
```

## 🔄 Common Integration Patterns

### 1. Salesforce to Database Sync

```javascript
// Process configuration for Salesforce sync
const salesforceSync = {
  name: "SF_to_DB_Account_Sync",
  components: [
    {
      type: "salesforce_connector",
      operation: "query",
      query: "SELECT Id, Name, BillingAddress FROM Account WHERE LastModifiedDate > YESTERDAY"
    },
    {
      type: "data_process",
      transformations: [
        { field: "Name", destination: "customer_name" },
        { field: "BillingAddress", destination: "billing_address" }
      ]
    },
    {
      type: "database_connector", 
      operation: "insert_update",
      table: "customers"
    }
  ]
};
```

### 2. File-based Integration

```javascript
// File processing workflow
const fileProcessing = {
  name: "CSV_Processing_Workflow",
  schedule: "0 */6 * * *", // Every 6 hours
  components: [
    {
      type: "file_connector",
      operation: "read",
      directory: "/incoming",
      filePattern: "*.csv"
    },
    {
      type: "data_process",
      validations: [
        { field: "email", rule: "email_format" },
        { field: "phone", rule: "phone_format" }
      ]
    },
    {
      type: "decision_shape",
      conditions: [
        { if: "record_count > 1000", then: "batch_process" },
        { else: "direct_process" }
      ]
    }
  ]
};
```

### 3. API Integration with Error Handling

```javascript
// Robust API integration
const apiIntegration = {
  name: "API_Integration_with_Retry",
  errorHandling: {
    maxRetries: 3,
    retryDelay: 5000,
    errorActions: [
      { condition: "timeout", action: "retry" },
      { condition: "500_error", action: "retry" },
      { condition: "400_error", action: "log_and_continue" }
    ]
  },
  components: [
    {
      type: "rest_connector",
      operation: "post",
      endpoint: "/api/customers",
      headers: {
        "Authorization": "Bearer ${token}",
        "Content-Type": "application/json"
      }
    }
  ]
};
```

## 🔐 Security Configuration

### Authentication Methods

#### API Token Authentication (Recommended)
```javascript
const config = {
  auth: {
    type: "api_token",
    username: "user@company.com",
    token: process.env.BOOMI_API_TOKEN
  }
};
```

#### OAuth 2.0 Authentication
```javascript
const config = {
  auth: {
    type: "oauth2",
    clientId: process.env.BOOMI_CLIENT_ID,
    clientSecret: process.env.BOOMI_CLIENT_SECRET,
    scope: "ProcessManagement ComponentLibrary"
  }
};
```

### Security Best Practices

1. **Use environment variables** for sensitive data
2. **Implement token rotation** for long-running processes  
3. **Enable audit logging** for all API calls
4. **Use least privilege principle** for API permissions
5. **Encrypt sensitive data** in process configurations
6. **Implement secure credential management**

## 🎯 Advanced Use Cases

### 1. Real-time Data Synchronization

```javascript
// Real-time sync with change detection
const realTimeSync = async () => {
  const changes = await detectDataChanges();
  
  if (changes.length > 0) {
    const process = await createBoomiProcess({
      name: "Real_Time_Sync_" + Date.now(),
      data: changes,
      priority: "high"
    });
    
    await executeProcess(process.id);
    await monitorExecution(process.id);
  }
};
```

### 2. Complex Data Transformation

```javascript
// Multi-step data transformation
const complexTransformation = {
  steps: [
    {
      name: "data_validation",
      rules: [
        "required_fields",
        "data_type_validation", 
        "business_rule_validation"
      ]
    },
    {
      name: "data_enrichment",
      lookups: [
        { table: "customer_master", key: "customer_id" },
        { api: "geo_location", field: "address" }
      ]
    },
    {
      name: "data_standardization",
      transformations: [
        { field: "phone", format: "e164" },
        { field: "date", format: "iso8601" }
      ]
    }
  ]
};
```

### 3. Process Orchestration

```javascript
// Multi-process orchestration
const orchestrateProcesses = async (workflow) => {
  const results = [];
  
  for (const step of workflow.steps) {
    if (step.type === 'parallel') {
      const parallelResults = await Promise.all(
        step.processes.map(p => executeBoomiProcess(p.id))
      );
      results.push(...parallelResults);
    } else {
      const result = await executeBoomiProcess(step.process.id);
      results.push(result);
      
      if (!result.success && step.required) {
        throw new Error(`Critical step failed: ${step.name}`);
      }
    }
  }
  
  return results;
};
```

## 🐛 Troubleshooting

### Common Issues

#### Authentication Failures
- **Issue**: "401 Unauthorized" or "403 Forbidden"
- **Solution**: Verify API token and permissions
- **Check**: Account ID format and token expiration

#### Process Execution Errors
- **Issue**: Process fails during execution
- **Solution**: Check connector configurations and data formats
- **Debug**: Use process execution logs and error details

#### Connection Timeouts
- **Issue**: API calls timing out
- **Solution**: Implement retry logic and increase timeout values
- **Monitor**: Network connectivity and Boomi service status

#### Data Mapping Issues
- **Issue**: Data transformation errors
- **Solution**: Validate source data structure and mapping rules
- **Test**: Use Boomi's built-in data viewer and test mode

### Debug Configuration

```json
{
  "debug": {
    "enabled": true,
    "logLevel": "DEBUG",
    "logAPIRequests": true,
    "logProcessExecutions": true,
    "logDataTransformations": true,
    "logFile": "logs/boomi-debug.log"
  }
}
```

### Process Monitoring Dashboard

```javascript
// Create monitoring dashboard
const createDashboard = async () => {
  const processes = await getAllProcesses();
  const dashboard = {
    totalProcesses: processes.length,
    activeProcesses: processes.filter(p => p.status === 'running').length,
    failedProcesses: processes.filter(p => p.status === 'error').length,
    avgExecutionTime: calculateAverageExecutionTime(processes)
  };
  
  updateDashboardUI(dashboard);
};
```

## 📊 Performance Optimization

### Process Performance

```javascript
// Optimize process performance
const optimizeProcess = {
  batchProcessing: {
    enabled: true,
    batchSize: 1000,
    parallelBatches: 3
  },
  caching: {
    enabled: true,
    cacheDuration: 3600, // 1 hour
    cacheKeys: ["customer_lookup", "product_catalog"]
  },
  connectionPooling: {
    enabled: true,
    maxConnections: 10,
    connectionTimeout: 30000
  }
};
```

### Resource Management

```javascript
// Monitor resource usage
const monitorResources = async () => {
  const atomStats = await getAtomStatistics();
  
  if (atomStats.memoryUsage > 80) {
    await alertOpsTeam("High memory usage on Atom", atomStats);
  }
  
  if (atomStats.queueSize > 1000) {
    await scaleProcessing(atomStats.queueSize);
  }
};
```

## 📚 Additional Resources

- [Dell Boomi Documentation](https://help.boomi.com/)
- [AtomSphere API Reference](https://help.boomi.com/bundle/developer_apis/page/int-AtomSphere_API_overview.html)
- [Boomi Community](https://community.boomi.com/)
- [Process Library](https://help.boomi.com/bundle/library/page/lib-Process_Library_overview.html)
- [Connector Guides](https://help.boomi.com/bundle/connectors/page/con-Connectors_overview.html)

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Test with your Boomi environment
4. Add comprehensive tests and documentation
5. Submit a pull request

## 📄 License

This integration is licensed under the MIT License - see the [LICENSE](../../LICENSE) file for details.

---

**Need help?** Check our [troubleshooting guide](../../docs/troubleshooting.md) or open an [issue](https://github.com/your-username/cursor-enterprise-connectors/issues).
