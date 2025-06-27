# Alerts to OWASP Top 10 Action

_A GitHub Action to filter and map your repository's security alerts to the OWASP Top 10 risks._

---

## 🚀 Why Use This Action?

In today's fast-paced development environment, understanding and mitigating security risks is paramount. This action helps organizations:

- **Identify Critical Exposure:** Quickly see if your repositories are exposed to the most critical web application security risks defined by the OWASP Top 10.
- **Prioritize Security Efforts:** Assist security officers in focusing on the highest-impact vulnerabilities.
- **Guide Engineering Teams:** Provide engineering managers with insights into application security gaps, facilitating targeted mentoring, learning, and skill development within their teams.

By automating the mapping of CodeQL alerts to OWASP Top 10, this action streamlines the process of gaining actionable security intelligence.

---

## ✨ Features

- Filters GitHub CodeQL code scanning alerts.
- Maps alerts to the corresponding OWASP Top 10 (2021) categories using CWE (Common Weakness Enumeration) data.
- Generates a `mapping.csv` file with the filtered and mapped alerts, ready for analysis.
- Generates an `alerts.json` file containing all open alerts in the organization, providing a comprehensive raw dataset.

---

## 🛠️ Usage

To use this action, add it as a step in your GitHub Actions workflow (`.github/workflows/main.yml` or similar).

### 🔧 Prerequisites

- GitHub CodeQL code scanning must be enabled in the repository to generate security alerts.
- The workflow token must have `security-events: read` permission.

### 📋 Example Workflow

```yaml
name: OWASP Top 10 Alerts Report

on:
  schedule:
    - cron: '0 0 * * *' # Runs daily at midnight UTC
  workflow_dispatch: # Allows manual triggering

jobs:
  build:
    runs-on: ubuntu-latest
    permissions:
      security-events: read # Grant read permission for security events
      contents: write        # Grant write permission to upload artifacts

    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Run Alerts to OWASP Top 10 Action
        uses: 'some-org/alerts-to-owasp10@v1' # Replace with the actual action path/version
        id: owasp_action
        with:
          # No inputs required for this action based on marketplace description
          # If any inputs are added later, they would go here.
          # e.g., github_token: ${{ secrets.GITHUB_TOKEN }}

      - name: Upload OWASP Mapping CSV
        uses: actions/upload-artifact@v4
        with:
          name: owasp-mapping-csv
          path: mapping.csv

      - name: Upload Raw Alerts JSON
        uses: actions/upload-artifact@v4
        with:
          name: raw-alerts-json
          path: alerts.json
