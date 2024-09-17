# CICD
This repository contains the Golang API, and we have implemented a CI/CD pipeline using GitHub Actions. The pipeline automatically deploys changes to AWS EKS upon a merge into the main branch. We are using an OIDC (OpenID Connect) provider to securely authenticate GitHub Actions to AWS without storing static credentials.

Git Strategy: Feature Branch Workflow

We have chosen the Feature Branch Workflow as our Git strategy. Here’s how it works:

	.	Branching:
	•	Every new feature or bug fix starts in a separate branch created from main.
	•	The branch name follows a convention like feature/<feature-name> or bugfix/<issue-number>.
	.	Development:
	•	Work on the feature happens in the feature branch. Multiple commits can be made to this branch as development continues.
	.	Pull Request (PR):
	•	Once the feature is complete, a pull request (PR) is opened to merge the feature branch into main.
	•	The pull request is reviewed by other developers before being merged.
	.	Merge:
	•	After the review is complete, the PR is merged into the main branch.
	•	Automated Deployment: The merge to main triggers the CI/CD pipeline, automatically deploying the changes to the AWS EKS cluster.

CI/CD Pipeline: GitHub Actions Workflow

We have implemented GitHub Actions workflows to handle CI/CD. The pipeline is triggered automatically when certain actions (like a push or merge) occur.

Key Workflow Actions:

	 1.	Build & Test:
	 2.	Every push to any branch triggers a build and test job to ensure the code works properly.
	 3.	Deploy:
	 4.	A merge into the main branch triggers the deployment workflow.
	 5.	The deployment uses the OIDC provider to authenticate securely to AWS and deploy the API to the EKS cluster.

 OIDC Authentication

Instead of using static AWS credentials, we use OIDC authentication for secure access. The OIDC provider allows GitHub Actions to assume an AWS IAM role using web identity federation. This eliminates the need for long-term credentials, enhancing security.

In the GitHub repository:

	1.	Add the OIDC role ARN to your repository secrets:
	2.	Go to your repository’s Settings → Secrets and variables → Actions.
	3.	Add a new secret: GITHUB_ACTIONS_ROLE_ARN with the value of the OIDC role ARN (from the Terraform outputs).
