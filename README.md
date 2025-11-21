# SmartUI SDK Sample for Selenium Ruby

Welcome to the SmartUI SDK sample for Selenium Ruby. This repository demonstrates how to integrate SmartUI visual regression testing with Selenium Ruby.

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

## 1. Prerequisites and Environment Setup

### Prerequisites

- Ruby 2.7 or higher
- Node.js (for SmartUI CLI)
- LambdaTest account credentials (for Cloud tests)
- Chrome browser (for Local tests)

### Environment Setup

**For Cloud:**
```bash
export LT_USERNAME='your_username'
export LT_ACCESS_KEY='your_access_key'
export PROJECT_TOKEN='your_project_token'
```

**For Local:**
```bash
export PROJECT_TOKEN='your_project_token'
```

## 2. Initial Setup and Dependencies

### Clone the Repository

```bash
git clone https://github.com/LambdaTest/smartui-ruby-selenium-sample
cd smartui-ruby-selenium-sample/sdk
```

### Install Dependencies

Install the required dependencies:

```bash
npm install @lambdatest/smartui-cli
gem install lambdatest-selenium-driver selenium-webdriver
```

**Dependencies included:**
- `@lambdatest/smartui-cli` - SmartUI CLI (via npm)
- `lambdatest-selenium-driver` - SmartUI SDK for Selenium Ruby (via gem)
- `selenium-webdriver` - Selenium WebDriver for Ruby (via gem)

**Note**: ChromeDriver is automatically managed by Selenium WebDriver.

### Create SmartUI Configuration

```bash
npx smartui config:create smartui-web.json
```

## 3. Steps to Integrate Screenshot Commands into Codebase

The SmartUI screenshot function is already implemented in the repository.

**Cloud Test** (`sdk/sdkCloud.rb`):
```ruby
driver.navigate.to "https://www.lambdatest.com"
Lambdatest::Selenium::Driver.smartui_snapshot(driver, "screenshot")
```

**Local Test** (`sdk/sdkLocal.rb`):
```ruby
driver.navigate.to "https://www.lambdatest.com"
Lambdatest::Selenium::Driver.smartui_snapshot(driver, "screenshot")
```

**Note**: The code is already configured and ready to use. You can modify the URL and screenshot name if needed.

## 4. Execution and Commands

### Local Execution

```bash
npx smartui exec ruby sdkLocal.rb
```

### Cloud Execution

```bash
npx smartui exec ruby sdkCloud.rb
```

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
