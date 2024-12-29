# Deploying Static Content to GitHub Pages

This repository contains a GitHub Actions workflow that automates the deployment of static content to GitHub Pages. This guide explains how the workflow is configured and how to use it.

## Workflow Overview
The workflow file `.github/workflows/deploy.yml` automates the deployment of static content to GitHub Pages whenever there are changes pushed to the `main` branch or when the workflow is manually triggered.

## Key Features
- **Automatic Deployment**: Deploys static content automatically on every push to the `main` branch.
- **Manual Deployment**: Allows manual triggering of deployments via the GitHub Actions tab.
- **Concurrency Control**: Ensures only one deployment runs at a time to avoid conflicts while allowing ongoing deployments to complete.
- **Secure Permissions**: Utilizes `GITHUB_TOKEN` with restricted permissions to securely deploy content.

## Prerequisites
1. Ensure your repository is public or has GitHub Pages enabled.
2. Configure GitHub Pages in the repository settings to use the `gh-pages` branch.

## Workflow Details
Here is a breakdown of the workflow steps:

### `on`
- **push**: The workflow triggers on pushes to the `main` branch.
- **workflow_dispatch**: The workflow can be manually triggered from the Actions tab.

### `permissions`
The workflow sets permissions for the `GITHUB_TOKEN` to:
- `contents: read`
- `pages: write`
- `id-token: write`

### `concurrency`
- The workflow ensures only one deployment runs at a time for the `pages` group.
- `cancel-in-progress: false` allows in-progress deployments to complete.

### `jobs`
The `deploy` job performs the deployment:

#### Environment
- **name**: `github-pages`
- **url**: Automatically set to the deployed GitHub Pages URL.

#### Steps
1. **Checkout Repository**:
   Uses `actions/checkout@v4` to clone the repository.
2. **Setup Pages**:
   Uses `actions/configure-pages@v5` to configure the GitHub Pages environment.
3. **Upload Artifact**:
   Uses `actions/upload-pages-artifact@v3` to upload the static content. The entire repository is uploaded by setting `path: '.'`.
4. **Deploy to GitHub Pages**:
   Uses `actions/deploy-pages@v4` to deploy the content. The deployed URL is stored in the `page_url` output variable.

## How to Use
1. Push changes to the `main` branch, and the workflow will automatically deploy the content to GitHub Pages.
2. Alternatively, navigate to the Actions tab in your repository, select the workflow, and trigger it manually using the "Run workflow" button.

This project is part of [Janis Adhikari's](https://roadmap.sh/projects/github-actions-deployment-workflow)  DevOps projects.