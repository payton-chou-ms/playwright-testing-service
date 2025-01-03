# Get Started Sample 

This sample uses a basic test to show how the service can speed up test suite completion with more parallel cloud browsers and publish test results and artifacts for easier troubleshooting.


If you have not yet created a workspace, please follow the [Get Started guide](../../README.md#get-started)


## Sample setup
1. Clone this sample:
    ```bash
    git clone https://github.com/microsoft/playwright-testing-service
    cd playwright-testing-service/samples/get-started
    ```

1. Install dependencies:
    ```bash
    npm install
    ```

1. Set up Authentication 

    To run your Playwright tests in your Microsoft Playwright Testing workspace, you need to authenticate the Playwright client where you are running the tests with the service. This could be your local dev machine or CI machine. To run tests from your local machine, you can use Azure CLI. Run this command to sign-in 
    
    ```CLI
    az login
    ```
    **NOTE**: If you are a part of multiple Microsoft Entra tenants, make sure you sign-in to the tenant where your workspace belongs. You can get the tenant id from Azure portal, see [Find your Microsoft Entra Tenant](https://learn.microsoft.com/en-us/azure/azure-portal/get-subscription-tenant-id#find-your-microsoft-entra-tenant). Once you get the id, sign in using the command `az login --tenant <TenantID>`

1. Create a `.env` file in the sample's directory and define the following environment variable: 
   In the [Playwright portal](https://aka.ms/mpt/portal), copy the command under **Add region endpoint in your set up** and set the following environment variable:
        ```bash
        PLAYWRIGHT_SERVICE_URL= # Paste region endpoint URL
        ```

## Run tests

Run Playwright tests against browsers managed by the service using the configuration you created above. You can run up to 50 parallel workers with the service

```bash
npx playwright test --config=playwright.service.config.ts --workers=20
```

# Add your own tests
## Generate tests

You can generate tests using the Playwright CLI.

```bash
npx playwright codegen https://demo.playwright.dev/todomvc
```
## Run tests locally with UI

You can run tests locally with the UI using the below command

```bash
npx playwright test --config=playwright.service.config.ts --workers=20 --ui
```

# Run tests in CI/CD pipeline
## Run tests in a GitHub workflow
1. Copy the file [get-started.yaml](.github/workflows/get-started.yml) to your repository's `.github/workflows` directory. 
1. Then follow the instructions in the article [Configure Playwright Service in a CI/CD pipeline](https://aka.ms/mpt/configure-pipeline).

## Run tests in a Azure Pipeline
1. Setup the Azure Pipeline using the file [azure-pipelines.yml](./azure-pipelines.yml) in your repository.
1. Then follow the instructions in the article [Configure Playwright Service in a CI/CD pipeline](https://aka.ms/mpt/configure-pipeline).

# Review Test Results
## Review test results with Snapshot and Recording

After running the tests, you can review the test results in the [Playwright portal](https://aka.ms/mpt/portal). You can view the test results, logs, and artifacts like screenshots and videos.

Add below config in playwritht.config.ts to enable snapshot and recording
```ts
  use: {
    trace: 'on-first-retry',
    screenshot: 'only-on-failure', // Capture screenshots only on failure
    video: 'retain-on-failure', // Record videos only on failure
  },
```
