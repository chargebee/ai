This repository was created from a starter template that includes essential configurations to help you ensure your codebase always remains secure by scanning for sensitive information such as API keys, access tokens, and other secrets hardcoded in the codebase.

## Starter kit files

### 1. **GitHub Actions Secrets Scanning Workflow**

- **Path**: `.github/workflows/secrets-scan.yml`
- **What It Is**: A GitHub Actions workflow that automatically scans for secrets in the files modified each time you open a pull request.
- **Why It's Here**: To detect hardcoded secrets in your codebase and prevent it from being exposed. If secrets are found, the workflow will fail, and you'll be notified of the findings so you can take action.

### 2. **Pre-commit Configuration File**

- **Path**: `.pre-commit-config.yaml`
- **What It Is**: This file configures pre-commit hooks to run checks on your code before every commit.
- **Why It's Here**: It ensures that secrets are scanned locally before any code is committed, preventing you from accidentally pushing secrets to your repository.

## Actions to be performed

**THESE FILES ARE INTEGRAL IN MAINTAINING A SECURE CODEBASE, DO NOT DELETE OR MODIFY THEM**

**Configure Pre-commit Hooks Locally**:

   - Install `pre-commit` on your machine:
     ```bash
     brew install pre-commit
     ```
   - Install the pre-commit hooks in your repository:
     ```bash
     cd /path/to/your/repo
     pre-commit install
     ```
   - Integrate Pre-commit in the build process:  
     > To ensure that git hooks are consistently configured, you must add the `pre-commit install` step to your build script.  
     > This is **mandatory** for all repositories. Please refer to [Hardcoded secrets prevention via Git pre-commit hooks](https://mychargebee.atlassian.net/wiki/spaces/ECS/pages/3335618745/Hardcoded+secrets+prevention+via+Git+pre-commit+hooks) for a detailed walkthrough.

Feel free to contact `#ask-security` if you face any issues.