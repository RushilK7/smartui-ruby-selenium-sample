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

## Testing with LambdaTest Hooks

This repository also includes examples for using SmartUI with LambdaTest Hooks integration. Hooks-based integration allows you to use SmartUI directly within your existing LambdaTest Cloud automation tests without requiring the SmartUI CLI.

### SDK vs Hooks: Which Approach to Use?

**SDK Approach (Recommended for Local Testing):**
- ✅ Works with both local and cloud execution
- ✅ Uses SmartUI CLI for configuration and execution
- ✅ Supports multiple browsers and viewports via `smartui-web.json`
- ✅ Better for CI/CD integration
- ✅ Requires `PROJECT_TOKEN` environment variable

**Hooks Approach (Recommended for Cloud-Only Testing):**
- ✅ Works only with LambdaTest Cloud Grid
- ✅ No CLI required - direct integration with LambdaTest
- ✅ Uses LambdaTest capabilities for configuration
- ✅ Better for existing LambdaTest automation suites
- ✅ Requires `LT_USERNAME` and `LT_ACCESS_KEY` environment variables

### Hooks Integration Setup

**Location:** See the `hooks` folder for hooks integration examples.

**Purpose:** Enhance visual regression capabilities in your LambdaTest web automation tests running on LambdaTest Cloud Grid.

**Documentation:** [LambdaTest Selenium Visual Regression Documentation](https://www.lambdatest.com/support/docs/selenium-visual-regression/).

### Hooks Setup Steps

#### 1. Install Dependencies

Install the required Ruby gems:

```bash
gem install selenium-webdriver
```

#### 2. Configure Environment Variables

Set your LambdaTest credentials:

```bash
export LT_USERNAME='your_username'
export LT_ACCESS_KEY='your_access_key'
```

#### 3. Configure Capabilities

In your test file (e.g., `hooks/smartui_hooks.rb`), configure the capabilities with SmartUI options:

```ruby
require 'selenium-webdriver'

USERNAME = ENV["LT_USERNAME"]
ACCESS_KEY = ENV["LT_ACCESS_KEY"]

options = Selenium::WebDriver::Options.chrome
options.browser_version = "119.0"
options.platform_name = "Windows 10"

lt_options = {
  username: USERNAME,
  accessKey: ACCESS_KEY,
  project: "Ruby Hooks Test",
  sessionName: "Ruby Test",
  build: "Ruby Job",
  w3c: true,
  plugin: "ruby-ruby",
  'smartUI.project': "Ruby-Project"  # Your SmartUI project name
}
options.add_option('LT:Options', lt_options)
```

#### 4. Connect to LambdaTest Grid

Create a WebDriver instance connected to LambdaTest Cloud:

```ruby
driver = Selenium::WebDriver.for(:remote,
  url: "https://hub.lambdatest.com/wd/hub",
  capabilities: options)
```

#### 5. Add Screenshot Hooks

Use `driver.execute_script()` to capture screenshots at any point in your test:

```ruby
# Navigate to your page
driver.navigate.to "https://www.lambdatest.com/visual-regression-testing"

# Take a screenshot with basic configuration
config = {
  'screenshotName' => 'SmartUI-Home',
  'fullPage' => true
}
driver.execute_script("smartui.takeScreenshot", config)

# Take a viewport screenshot (visible area only)
viewport_config = {
  'screenshotName' => 'SmartUI-Home-Viewport',
  'fullPage' => false
}
driver.execute_script("smartui.takeScreenshot", viewport_config)
```

#### 6. Run the Test

Execute your test script:

```bash
cd hooks
ruby smartui_hooks.rb
```

### Advanced Hooks Examples

#### Multiple Screenshots in One Test

```ruby
driver.navigate.to "https://www.lambdatest.com"

# Screenshot 1: Homepage
config1 = {
  'screenshotName' => 'homepage',
  'fullPage' => true
}
driver.execute_script("smartui.takeScreenshot", config1)

# Navigate and take another screenshot
driver.navigate.to "https://www.lambdatest.com/pricing"
config2 = {
  'screenshotName' => 'pricing-page',
  'fullPage' => true
}
driver.execute_script("smartui.takeScreenshot", config2)
```

#### Screenshot with Custom Options

```ruby
config = {
  'screenshotName' => 'homepage-custom',
  'fullPage' => true,
  'ignore' => ['antialiasing', 'colors']
}
driver.execute_script("smartui.takeScreenshot", config)
```

### Hooks Configuration Options

The SmartUI hooks support various configuration options:

- **screenshotName**: Name for the screenshot (required)
- **fullPage**: Set to `true` for full-page screenshot, `false` for viewport only
- **ignore**: Array of visual artifacts to ignore (`"antialiasing"`, `"colors"`, etc.)

### View Hooks Results

After running your hooks-based tests, visit the [LambdaTest Automation Dashboard](https://automation.lambdatest.com/) to view:
- Test execution status
- Screenshots captured
- Visual comparison results
- Build and session details

Navigate to your SmartUI project in the [SmartUI Dashboard](https://smartui.lambdatest.com/) to see detailed visual regression results.

## View Results

After running the tests, visit your SmartUI project dashboard to view the captured screenshots and compare them with baseline builds.

## More Information

For detailed onboarding instructions, see the [SmartUI Selenium Ruby Onboarding Guide](https://www.lambdatest.com/support/docs/smartui-onboarding-selenium-ruby/).
