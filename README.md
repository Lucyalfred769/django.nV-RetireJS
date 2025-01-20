# django.nV-RetireJS  

This project demonstrates how to scan for vulnerabilities in JavaScript libraries using **RetireJS** with a vulnerable Django application. It includes setting up the project locally, performing security scans, and automating the process using GitHub Actions.

---

## Prerequisites  

### Install Required Tools  
1. **Node.js and npm**  
    Install Node.js from the [official site](https://nodejs.org/). After installation, verify versions:
    ```bash
    node -v
    npm -v
    ```

2. **RetireJS**  
    Install RetireJS globally using npm:
    ```bash
    npm install -g retire
    retire -v  # Confirm installation
    ```

---

## Local Setup  

### Step 1: Clone the Repository  
Fork this repository, then clone it:
```bash
git clone https://github.com/Lucyalfred769/django.nV-RetireJS.git
cd django.nV-RetireJS
```

### Step 2: Initialize Git Repository  
If not already initialized:
```bash
git init
```

### Step 3: Organize Ignored Files  
To keep your repository clean, add commonly ignored files and folders to `.gitignore`:
```bash
echo "__pycache__/" >> .gitignore
echo "node_modules/" >> .gitignore
echo "*.log" >> .gitignore
echo "*.json" >> .gitignore
```
Verify the `.gitignore` file:
```bash
cat .gitignore
```

---

## Security Scan  

### Step 1: Run RetireJS Locally  
Perform a vulnerability scan and output results in JSON format:
```bash
retire --outputformat json --outputpath retirejs-report.json
```

### Step 2: Verify Scan Results  
Ensure the `retirejs-report.json` file is generated:
```bash
ls
cat retirejs-report.json
```

---

## Automating with GitHub Actions  
### GitHub Actions Workflow for RetireJS
  
Create a folder for GitHub Actions workflows:
```bash
mkdir -p .github/workflows
```

Create the workflow file:
```bash
nano .github/workflows/retirejs-scan.yml
```

Add the following contents to automate RetireJS scans:
```yaml
name: RetireJS Scan

on:
    push:
        branches:
            - main
    pull_request:

jobs:
    scan:
        runs-on: ubuntu-latest
        steps:
            - name: Checkout Code
                uses: actions/checkout@v3

            - name: Set up Node.js
                uses: actions/setup-node@v3
                with:
                    node-version: '18'

            - name: Install RetireJS
                run: npm install -g retire

            - name: Run RetireJS Scan
                run: retire --outputformat json --outputpath retirejs-report.json
```

Save and exit the editor.

### Commit and Push Change
Add your changes to the repository:
```bash
git add .
git commit -m "Initial commit with RetireJS scanning workflow"
git branch -M main
git remote add origin <your-repository-url>
git push -u origin main
```

### Step 5: Trigger Workflow  
Push any updates or open a pull request to trigger the GitHub Actions workflow. View the scan results under the **Actions** tab in your GitHub repository.

---

## Importance of Local Testing  
Testing locally before moving to the pipeline is crucial as it helps identify and fix issues early, ensuring that the automated pipeline runs smoothly without interruptions. This practice saves time and resources by catching potential problems before they reach the CI/CD pipeline.

---

## Summary  
This project integrates RetireJS into a DevSecOps workflow for detecting vulnerabilities in JavaScript libraries. It starts with local scans, organizes outputs, and automates scans through GitHub Actions, ensuring security throughout the development lifecycle.
