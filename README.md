🚀 GitHub Actions Workflow Learning Repository
This repository is created to learn, practice, and understand GitHub Actions from basics to advanced concepts using real, working workflows.
The goal is to understand how CI/CD works, not just how to write YAML.

📌 What You’ll Learn
By going through this repository, you will learn:

✅ What GitHub Actions is and how it works
✅ Workflow structure (workflow → jobs → steps)
✅ Event triggers (push, pull_request, workflow_dispatch)
✅ Manual input variables
✅ Environment variables (repo & environment scoped)
✅ Secrets handling
✅ GitHub context variables
✅ Job dependencies using needs
✅ Step & job output variables
✅ Debugging workflows correctly
✅ Best practices used in real projects


📂 Repository Structure
.github/
└── workflows/
    ├── basic-workflow.yml
    ├── manual-inputs.yml
    ├── env-and-vars.yml
    ├── github-context.yml
    ├── reuse-output-variables.yml
    └── multi-job-pipeline.yml

Each workflow demonstrates one concept clearly, without mixing everything at once.

✅ What is GitHub Actions?
GitHub Actions is a CI/CD platform that lets you automate tasks like:

Running tests
Validating code
Building and deploying applications

Workflows are defined using YAML and live inside:
.github/workflows/


🧱 Basic Workflow Structure
Every GitHub Actions workflow follows this structure:
Workflow
 └── Jobs
      └── Job
           └── Steps
                ├── uses (actions)
                └── run (commands)

Example:
YAMLname: Basic Workflowon:  workflow_dispatchjobs:  example_job:    runs-on: ubuntu-latest    steps:      - run: echo "Hello GitHub Actions"``Show more lines

🎯 Event Triggers Used





























TriggerPurposepushRun workflow when code is pushedpull_requestRun workflow for PR validationworkflow_dispatchRun workflow manuallyscheduleNightly or periodic runsreleaseTrigger on release

✋ Manual Input Variables (workflow_dispatch)
Manual inputs allow users to pass values at runtime from the GitHub UI.
Example:
YAMLon:  workflow_dispatch:    inputs:      environment:        description: "Select environment"        required: true        type: choice        options:          - test          - staging          - production``Show more lines
Access input:
YAML${{ inputs.environmentShow more lines

🌍 Variables in GitHub Actions
Variable Types Covered





























TypeAccessRepository variables${{ vars.VAR_NAME }}Environment variables$VAR_NAMESecrets${{ secrets.SECRET_NAME }}GitHub context${{ github.* }}Manual inputs${{ inputs.* }}

🔐 Secrets
Secrets store sensitive information like tokens and passwords.
Defined in:
Settings → Secrets and variables → Actions → Secrets

Usage:
YAML${{ secrets.API_TOKEN }}Show more lines
Secrets are masked in logs automatically.

🧠 GitHub Context Variables
GitHub provides read‑only metadata about the workflow run.
Commonly used:





























VariableDescription${{ github.repository }}Repository name${{ github.actor }}Who triggered the workflow${{ github.workflow }}Workflow name${{ github.job }}Job name${{ github.event_name }}Trigger event
Example:
YAML- run: echo "Triggered by ${{ github.actor }}"Show more lines

🔁 Multiple Jobs & Dependencies (needs)
Jobs run in parallel by default.
To run jobs sequentially, use:
YAMLneeds: previous_job_nameShow more lines
Example:
YAMLjobs:  build:    runs-on: ubuntu-latest  test:    needs: build    runs-on: ubuntu-latestShow more lines

📤 Output Variables
Output variables allow:

One step to pass data to another step
One job to pass data to another job

Example (step output):
YAML- name: Set value  id: set_value  run: echo "result=success" >> $GITHUB_OUTPUTShow more lines
Usage:
YAML${{ steps.set_value.outputs.result }}Show more lines

🐛 Debugging Tips
To debug environment variables:
YAML- name: Debug Environment  run: env | sortShow more lines
This shows all variables available at runtime.

✅ Best Practices Followed

✔ One concept per workflow
✔ Clear names for jobs and steps
✔ Proper use of environments
✔ Secure handling of secrets
✔ Clean YAML formatting
✔ Re‑runnable workflows
✔ Real‑world automation patterns


🧪 How to Use This Repository

Fork or clone the repository
Open Actions tab
Run workflows using Run workflow
Observe logs step by step
Modify workflows and experiment


📘 Who This Repo Is For
✅ Beginners learning GitHub Actions
✅ Automation test engineers
✅ DevOps learners
✅ QA engineers moving into CI/CD
✅ Interview preparation
