## 🚀 Continuous Integration with GitHub Actions

This repository uses **GitHub Actions** for Continuous Integration (CI). The workflow:
- **Triggers on every push and pull request** to the `main` branch
- **Sets up a Python environment**
- **Installs dependencies**
- **Runs linting (flake8)**
- **Executes unit tests (pytest)**

### 📄 CI Workflow Configuration

The following `.yaml` file is located in `.github/workflows/ci.yml`:

```yaml
name: Continuous Integration

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v3

      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: "3.9"

      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          pip install -r requirements.txt

      - name: Lint with flake8
        run: |
          pip install flake8
          flake8 .

      - name: Run tests with pytest
        run: |
          pip install pytest
          pytest tests/
```

> 🛠 How to Set Up CI
1. Create the workflow file
    - Add the above .yaml file inside .github/workflows/ci.yml

2. Commit & Push
```sh
git add .github/workflows/ci.yml
git commit -m "Add GitHub Actions CI workflow"
git push origin main
```

3. Check the Workflow
    - Go to your GitHub repository → Actions tab
    - Ensure that the CI pipeline runs successfully