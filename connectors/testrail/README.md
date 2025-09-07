# TestRail Cursor Integration

Integration guide for connecting Cursor IDE with TestRail test management platform for enhanced test case generation, automation, and comprehensive testing workflow management.

## ✨ Features

- **Test Case Generation**: AI-powered test case creation from code analysis
- **Test Run Automation**: Automated test execution and result reporting
- **Result Reporting**: Real-time test result updates and reporting
- **TestRail API Integration**: Full access to TestRail's comprehensive API
- **Test Plan Management**: Create and manage test plans and milestones
- **Requirement Traceability**: Link test cases to requirements and code
- **Custom Field Support**: Work with custom fields and configurations

## 📋 Prerequisites

- Cursor IDE installed
- TestRail instance (cloud or on-premise) with appropriate permissions
- TestRail API access enabled
- API key or OAuth credentials
- Node.js 18+ or Python 3.8+

## 🚀 Quick Start

### 1. Enable TestRail API Access

#### Enable API in TestRail
1. Log into TestRail as Administrator
2. Navigate to **Administration** → **Site Settings**  
3. Go to **API** tab
4. Enable **Enable API** checkbox
5. Save settings

#### Generate API Key
1. Go to **My Settings** → **API Keys**
2. Click **Generate Key**
3. Copy the generated API key
4. Note: API keys are user-specific and inherit user permissions

### 2. Configure Authentication

```bash
# Copy configuration template
cp config/config.example.json config/config.json
```

Edit `config/config.json`:

```json
{
  "testrail": {
    "baseUrl": "https://your-company.testrail.io",
    "username": "your-email@your-company.com", 
    "apiKey": "YOUR_API_KEY",
    "projectId": 1,
    "suiteId": 1,
    "defaultAssignee": "user@company.com",
    "oauth": {
      "clientId": "YOUR_CLIENT_ID",
      "clientSecret": "YOUR_CLIENT_SECRET",
      "redirectUri": "http://localhost:8080/oauth/callback"
    }
  }
}
```

### 3. Install Dependencies

```bash
# Using npm
npm install testrail-api axios

# Using pip (for Python)
pip install testrail-python requests
```

### 4. Test Connection

```bash
# Test TestRail connection
node scripts/test_connection.js

# Test specific project
python scripts/test_connection.py --project-id 1
```

## 📖 Usage Examples

### Test Case Generation

#### Generate Test Cases from Code

```
🤖 Cursor Prompt: "Generate test cases for the user authentication function with edge cases and security testing"
```

Generated test cases:
```json
[
  {
    "title": "Valid login with correct credentials",
    "type_id": 1,
    "priority_id": 3,
    "estimate": "5m",
    "custom_steps_separated": [
      {
        "content": "Enter valid username and password",
        "expected": "User is successfully authenticated and redirected to dashboard"
      }
    ]
  },
  {
    "title": "Login attempt with invalid password",
    "type_id": 1, 
    "priority_id": 2,
    "custom_steps_separated": [
      {
        "content": "Enter valid username with incorrect password",
        "expected": "Error message displayed: 'Invalid credentials'"
      }
    ]
  }
]
```

#### API Testing Test Cases

```
🤖 Cursor Prompt: "Create API test cases for the REST endpoints in user-service.js with status code validation"
```

### Automated Test Execution

#### Run Test Suite and Report Results

```javascript
// Automated test execution with result reporting
const runTestSuite = async (suiteId, runName) => {
  // Create test run
  const testRun = await testrail.addRun(projectId, {
    suite_id: suiteId,
    name: runName,
    description: "Automated test run from Cursor integration",
    assignedto_id: userId
  });
  
  // Execute tests and collect results
  const testResults = await executeTests();
  
  // Report results to TestRail
  for (const result of testResults) {
    await testrail.addResult(result.testId, {
      status_id: result.passed ? 1 : 5, // 1=Passed, 5=Failed
      comment: result.message,
      elapsed: result.duration
    });
  }
  
  return testRun;
};
```

### Test Plan Management

#### Create Test Plan with Milestones

```javascript
// Create comprehensive test plan
const createTestPlan = async (planData) => {
  const testPlan = await testrail.addPlan(projectId, {
    name: planData.name,
    description: planData.description,
    milestone_id: planData.milestoneId,
    entries: [
      {
        suite_id: planData.suiteId,
        name: "Regression Tests",
        assignedto_id: planData.assigneeId,
        include_all: false,
        case_ids: planData.testCaseIds
      }
    ]
  });
  
  return testPlan;
};
```

## 🛠️ Available Scripts

| Script | Description |
|--------|-------------|
| `scripts/testcases/generate.js` | Generate test cases from code |
| `scripts/testcases/import.js` | Import test cases to TestRail |
| `scripts/testruns/create_run.js` | Create and execute test runs |
| `scripts/testruns/report_results.js` | Report test results |
| `scripts/testplans/create_plan.js` | Create test plans |
| `scripts/milestones/manage.js` | Manage project milestones |
| `scripts/reports/generate.js` | Generate custom reports |
| `scripts/sync/requirements.js` | Sync with requirements |

## 📁 Project Structure

```
testrail/
├── README.md
├── config/
│   ├── config.example.json     # Configuration template
│   ├── test-templates/         # Test case templates
│   └── custom-fields.json      # Custom field definitions
├── extension/
│   ├── extension.js            # Cursor extension entry point
│   └── commands/               # Custom commands
├── scripts/
│   ├── testcases/              # Test case management
│   ├── testruns/               # Test run operations
│   ├── testplans/              # Test plan management
│   ├── milestones/             # Milestone management
│   ├── reports/                # Reporting utilities
│   └── sync/                   # Synchronization tools
├── templates/
│   ├── testcases/              # Test case templates
│   ├── testplans/              # Test plan templates
│   └── reports/                # Report templates
├── examples/
│   ├── basic-testing/          # Basic testing workflows
│   ├── automated-reporting/    # Automated reporting examples
│   └── api-testing/            # API testing examples
└── tests/
    ├── unit/                   # Unit tests
    └── integration/            # Integration tests
```

## 🧪 Test Case Templates

### 1. Unit Test Template

```json
{
  "template_name": "unit_test",
  "fields": {
    "title": "Unit Test: {function_name}",
    "type_id": 1,
    "priority_id": 2,
    "template": [
      "Setup test data and mocks",
      "Call the function with test inputs", 
      "Assert expected outputs",
      "Verify no side effects"
    ]
  }
}
```

### 2. Integration Test Template

```json
{
  "template_name": "integration_test",
  "fields": {
    "title": "Integration Test: {component_name}",
    "type_id": 2,
    "priority_id": 3,
    "template": [
      "Setup test environment",
      "Configure component dependencies",
      "Execute integration scenario",
      "Validate end-to-end functionality",
      "Cleanup test data"
    ]
  }
}
```

### 3. API Test Template

```json
{
  "template_name": "api_test",
  "fields": {
    "title": "API Test: {endpoint_name}",
    "type_id": 3,
    "priority_id": 2,
    "custom_expected": "HTTP {status_code} with valid response schema",
    "template": [
      "Send {http_method} request to {endpoint}",
      "Include required headers and authentication",
      "Validate response status code",
      "Verify response schema and data",
      "Check response time constraints"
    ]
  }
}
```

## 🔄 Automated Workflows

### 1. CI/CD Integration

```yaml
# .github/workflows/testrail-integration.yml
name: TestRail Integration
on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  test-and-report:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      
      - name: Run Tests
        run: |
          npm test -- --reporter json --outputFile test-results.json
          
      - name: Report to TestRail
        env:
          TESTRAIL_URL: ${{ secrets.TESTRAIL_URL }}
          TESTRAIL_USERNAME: ${{ secrets.TESTRAIL_USERNAME }}
          TESTRAIL_API_KEY: ${{ secrets.TESTRAIL_API_KEY }}
        run: |
          node scripts/testruns/report_results.js \
            --results test-results.json \
            --run-id ${{ github.run_id }}
```

### 2. Automated Test Case Creation

```javascript
// Auto-generate test cases from code changes
const generateTestCasesFromDiff = async (gitDiff) => {
  const changedFunctions = parseGitDiff(gitDiff);
  const testCases = [];
  
  for (const func of changedFunctions) {
    const aiGeneratedTests = await generateTestCases(func);
    
    for (const test of aiGeneratedTests) {
      const testCase = await testrail.addCase(sectionId, {
        title: test.title,
        type_id: getTestTypeId(test.type),
        priority_id: getPriorityId(test.priority),
        custom_steps_separated: test.steps,
        refs: `GitHub:${func.commitSha}`
      });
      
      testCases.push(testCase);
    }
  }
  
  return testCases;
};
```

### 3. Smart Test Execution

```javascript
// Intelligent test selection based on code changes
const selectRelevantTests = async (changedFiles) => {
  const allTests = await testrail.getCases(projectId, { suite_id: suiteId });
  const relevantTests = [];
  
  for (const test of allTests) {
    const coverage = await getTestCoverage(test.id);
    const isRelevant = changedFiles.some(file => 
      coverage.files.includes(file)
    );
    
    if (isRelevant) {
      relevantTests.push(test);
    }
  }
  
  return relevantTests;
};
```

## 🔐 Security and Permissions

### Required Permissions

#### Minimum Permissions
- **Projects**: View project details
- **Test Cases**: View and add test cases
- **Test Runs**: Create and manage test runs
- **Results**: Add test results

#### Advanced Permissions
- **Test Plans**: Create and manage test plans
- **Milestones**: Create and manage milestones
- **Reports**: Generate and view reports
- **Users**: View user information

### Security Best Practices

1. **Use API keys** instead of passwords
2. **Implement key rotation** policies
3. **Store credentials securely** in environment variables
4. **Use HTTPS only** for API communication
5. **Implement rate limiting** for API calls
6. **Enable audit logging** for all operations

## 🎯 Advanced Use Cases

### 1. Test Metrics and Analytics

```javascript
// Generate comprehensive test metrics
const generateTestMetrics = async (projectId, timeframe) => {
  const runs = await testrail.getRuns(projectId, { created_after: timeframe });
  const metrics = {
    totalRuns: runs.length,
    totalTests: 0,
    passRate: 0,
    avgExecutionTime: 0,
    topFailures: []
  };
  
  for (const run of runs) {
    const tests = await testrail.getTests(run.id);
    metrics.totalTests += tests.length;
    
    const results = await testrail.getResults(run.id);
    const passed = results.filter(r => r.status_id === 1).length;
    metrics.passRate = (passed / results.length) * 100;
  }
  
  return metrics;
};
```

### 2. Requirement Traceability

```javascript
// Link test cases to requirements
const linkTestsToRequirements = async (testCases, requirements) => {
  for (const testCase of testCases) {
    const relatedReqs = findRelatedRequirements(testCase, requirements);
    
    if (relatedReqs.length > 0) {
      await testrail.updateCase(testCase.id, {
        refs: relatedReqs.map(req => `REQ-${req.id}`).join(', ')
      });
    }
  }
};
```

### 3. Risk-Based Testing

```javascript
// Prioritize tests based on risk assessment
const prioritizeTestsByRisk = async (testCases, riskAssessment) => {
  const prioritizedTests = testCases.map(test => {
    const risk = calculateRisk(test, riskAssessment);
    return {
      ...test,
      risk_score: risk,
      priority: getRiskBasedPriority(risk)
    };
  });
  
  return prioritizedTests.sort((a, b) => b.risk_score - a.risk_score);
};
```

## 🐛 Troubleshooting

### Common Issues

#### API Authentication Issues
- **Issue**: "Authentication failed" (401)
- **Solution**: Verify username/email and API key
- **Check**: API access enabled in TestRail settings

#### Test Case Creation Failures
- **Issue**: "Field validation error" (400)
- **Solution**: Verify required fields and valid values
- **Check**: Custom field configurations and types

#### Performance Issues
- **Issue**: Slow API responses
- **Solution**: Implement pagination and caching
- **Monitor**: API rate limits and response times

#### Data Sync Issues
- **Issue**: Test results not updating
- **Solution**: Verify test case IDs and run status
- **Debug**: Check API response logs and error messages

### Debug Configuration

```json
{
  "debug": {
    "enabled": true,
    "logLevel": "DEBUG", 
    "logAPIRequests": true,
    "logAPIResponses": true,
    "logTestExecution": true,
    "logFile": "logs/testrail-debug.log"
  }
}
```

### Health Check Script

```javascript
// TestRail connection health check
const healthCheck = async () => {
  try {
    const user = await testrail.getUser();
    const projects = await testrail.getProjects();
    
    console.log(`✅ Connected as: ${user.name}`);
    console.log(`✅ Access to ${projects.length} projects`);
    
    return { status: 'healthy', user, projects: projects.length };
  } catch (error) {
    console.error(`❌ Health check failed: ${error.message}`);
    return { status: 'unhealthy', error: error.message };
  }
};
```

## 📊 Reporting and Analytics

### Custom Report Generation

```javascript
// Generate custom test execution report
const generateCustomReport = async (runId) => {
  const run = await testrail.getRun(runId);
  const tests = await testrail.getTests(runId);
  const results = await testrail.getResults(runId);
  
  const report = {
    run_info: {
      name: run.name,
      created_on: run.created_on,
      completed_on: run.completed_on
    },
    statistics: {
      total: tests.length,
      passed: results.filter(r => r.status_id === 1).length,
      failed: results.filter(r => r.status_id === 5).length,
      blocked: results.filter(r => r.status_id === 2).length
    },
    execution_time: {
      total: results.reduce((sum, r) => sum + (r.elapsed || 0), 0),
      average: results.reduce((sum, r) => sum + (r.elapsed || 0), 0) / results.length
    }
  };
  
  return report;
};
```

### Test Trend Analysis

```javascript
// Analyze test trends over time
const analyzeTestTrends = async (projectId, months) => {
  const startDate = new Date();
  startDate.setMonth(startDate.getMonth() - months);
  
  const runs = await testrail.getRuns(projectId, {
    created_after: Math.floor(startDate.getTime() / 1000)
  });
  
  const trends = runs.map(run => ({
    date: run.created_on,
    pass_rate: calculatePassRate(run),
    execution_time: calculateAvgExecutionTime(run)
  }));
  
  return trends;
};
```

## 📚 Additional Resources

- [TestRail API Documentation](https://www.gurock.com/testrail/docs/api)
- [TestRail User Guide](https://www.gurock.com/testrail/docs)
- [Test Case Management Best Practices](https://www.gurock.com/testrail/resources)
- [TestRail Integrations](https://www.gurock.com/testrail/integrations)

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Test with your TestRail instance
4. Add comprehensive tests and documentation
5. Submit a pull request

## 📄 License

This integration is licensed under the MIT License - see the [LICENSE](../../LICENSE) file for details.

---

**Need help?** Check our [troubleshooting guide](../../docs/troubleshooting.md) or open an [issue](https://github.com/your-username/cursor-enterprise-connectors/issues).
