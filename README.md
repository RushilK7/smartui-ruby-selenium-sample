# SmartUI SDK Sample for Selenium Ruby

Welcome to the SmartUI SDK sample for Selenium Ruby. This repository demonstrates how to integrate SmartUI visual regression testing with Selenium Ruby.

## Prerequisites

- Ruby 2.7 or higher
- Node.js (for SmartUI CLI)
- LambdaTest account credentials (for Cloud tests)
- Chrome browser (for Local tests)

## Repository Structure

```
smartui-ruby-selenium-sample/
├── sdk/
│   ├── sdkCloud.rb          # Cloud test
│   ├── sdkLocal.rb          # Local test
│   ├── ignore_select.rb     # Example with ignore options
│   ├── package.json         # SmartUI CLI dependency
│   └── smartui-web.json     # SmartUI config (create with npx smartui config:create)
└── hooks/                    # Hooks integration examples
    └── smartui_hooks.rb
```

## Quick Start

### Local Execution

1. **Clone the repository:**
   ```bash
   git clone https://github.com/LambdaTest/smartui-ruby-selenium-sample
   cd smartui-ruby-selenium-sample/sdk
   ```

2. **Install dependencies:**
   ```bash
   npm install @lambdatest/smartui-cli
   gem install lambdatest-selenium-driver selenium-webdriver
   ```

3. **Set your Project Token:**
   ```bash
   export PROJECT_TOKEN='your_project_token'
   ```

4. **Create SmartUI config:**
   ```bash
   npx smartui config:create smartui-web.json
   ```

5. **Run the test:**
   ```bash
   npx smartui exec ruby sdkLocal.rb
   ```

### Cloud Execution

1. **Clone the repository:**
   ```bash
   git clone https://github.com/LambdaTest/smartui-ruby-selenium-sample
   cd smartui-ruby-selenium-sample/sdk
   ```

2. **Install dependencies:**
   ```bash
   npm install @lambdatest/smartui-cli
   gem install lambdatest-selenium-driver selenium-webdriver
   ```

3. **Set your credentials:**
   ```bash
   export LT_USERNAME='your_username'
   export LT_ACCESS_KEY='your_access_key'
   export PROJECT_TOKEN='your_project_token'
   ```

4. **Create SmartUI config:**
   ```bash
   npx smartui config:create smartui-web.json
   ```

5. **Run the test:**
   ```bash
   npx smartui exec ruby sdkCloud.rb
   ```

## Dependencies

The project uses the following key dependencies:

- `@lambdatest/smartui-cli` - SmartUI CLI (via npm)
- `lambdatest-selenium-driver` - SmartUI SDK for Selenium Ruby (via gem)
- `selenium-webdriver` - Selenium WebDriver for Ruby (via gem)

## Test Files

### Cloud Test (`sdk/sdkCloud.rb`)

- Connects to LambdaTest Cloud using Selenium Remote WebDriver
- Reads credentials from environment variables (`LT_USERNAME`, `LT_ACCESS_KEY`)
- Takes screenshot with name: `screenshot`

### Local Test (`sdk/sdkLocal.rb`)

- Runs Selenium locally using Chrome
- Requires Chrome browser installed
- Takes screenshot with name: `screenshot`

### Ignore Example (`sdk/ignore_select.rb`)

- Demonstrates how to use ignore options in SmartUI snapshots
- Shows how to exclude specific DOM elements from visual comparison

## View Results

After running the tests, visit your SmartUI project dashboard to view the captured screenshots and compare them with baseline builds.

## More Information

For detailed onboarding instructions, see the [SmartUI Selenium Ruby Onboarding Guide](https://www.lambdatest.com/support/docs/smartui-onboarding-selenium-ruby/).
