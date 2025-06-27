Alerts to OWASP Top 10 Action
A GitHub Action to filter and map your repository's security alerts to the OWASP Top 10 risks.

🚀 Why Use This Action?
In today's fast-paced development environment, understanding and mitigating security risks is paramount. This action helps organizations:

Identify Critical Exposure: Quickly see if your repositories are exposed to the most critical web application security risks defined by the OWASP Top 10.

Prioritize Security Efforts: Assist security officers in focusing on the highest-impact vulnerabilities.

Guide Engineering Teams: Provide engineering managers with insights into application security gaps, facilitating targeted mentoring, learning, and skill development within their teams.

By automating the mapping of CodeQL alerts to OWASP Top 10, this action streamlines the process of gaining actionable security intelligence.

✨ Features
Filters GitHub CodeQL code scanning alerts.

Maps alerts to the corresponding OWASP Top 10 2021 categories using Common Weakness Enumeration (CWE) data.

Generates a CSV file (mapping.csv) with the filtered and mapped alerts, ready for analysis.

Generates a JSON file (alerts.json) containing all open alerts in the organization, providing a comprehensive raw dataset.

🛠️ Usage
To use this action, add it as a step in your GitHub Actions workflow (.github/workflows/main.yml or similar).

Prerequisites
Ensure your repository has GitHub CodeQL code scanning enabled to generate security alerts.

The workflow token needs security_events: read permission to access security alerts.

Example Workflow
Here's a basic example of how to integrate the alerts-to-owasp10 action into your workflow:

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
      contents: write # Grant write permission to upload artifacts

    steps:
    - name: Checkout repository
      uses: actions/checkout@v4

    - name: Run Alerts to OWASP Top 10 Action
      uses: 'some-org/alerts-to-owasp10@v1' # Replace with the actual action path/version
      id: owasp_action
      with:
        # No inputs required for this action based on marketplace description
        # If any inputs are added later, they would go here.
        # e.g., github_token: ${{ secrets.GITHUB_TOKEN }} # (If not using default GITHUB_TOKEN)

    - name: Upload OWASP Mapping CSV
      uses: actions/upload-artifact@v4
      with:
        name: owasp-mapping-csv
        path: mapping.csv # Path to the generated CSV file

    - name: Upload Raw Alerts JSON
      uses: actions/upload-artifact@v4
      with:
        name: raw-alerts-json
        path: alerts.json # Path to the generated JSON file

Note: Replace 'some-org/alerts-to-owasp10@v1' with the correct owner/repository/tag if this action is not officially under marketplace.

⚙️ Outputs
The action produces the following files in your workflow's working directory, which you can then upload as artifacts:

mapping.csv: A CSV file containing a filtered list of GitHub security alerts that are related to the OWASP Top 10, with their respective OWASP categories.

alerts.json: A JSON file containing an unfiltered list of all open security alerts found across the organization's repositories.

🤝 Contributing
Contributions are welcome! If you find a bug or have a feature request, please open an issue.

📄 License
This action is released under the MIT License.
