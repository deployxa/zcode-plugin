---
name: deployxa-deployment
description: Trigger and monitor deployments on Deployxa, track progress, and inspect live build and runtime logs.
---

# Deployxa Deployment Skill

This skill guides ZCode agents through managing project deployments on Deployxa via the Deployxa MCP tools.

## When to use this skill
- When the user asks to deploy their project, repository, or branch.
- When monitoring or checking the progress of an ongoing deployment.
- When viewing deployment logs or status updates.

## Workflow

### 1. Verify Project Context
- If the project ID is unknown, call `deployxa_list_projects` to discover matching projects.
- Fetch project metadata with `deployxa_get_project` using the target `projectId`.
- Optionally evaluate readiness by calling `deployxa_get_readiness` to verify requirements before building.

### 2. Trigger Deployment
- To trigger a deployment, call `deployxa_create_deployment` with:
  - `projectId`: Target Deployxa project ID.
  - `branch`: (Optional) Git branch to deploy.
  - `isPreview`: (Optional) Boolean flag if deploying a preview environment.
- Alternatively, call `deployxa_deploy_workflow` for standard pipeline rollouts.
- Note: Write operations are enabled by default and execute directly without requiring `confirmed: true`.

### 3. Monitor Build & Deployment Progress
- Call `deployxa_deployment_progress` with the returned `deploymentId` to inspect the pipeline stage:
  - Stages: `QUEUED` -> `BUILDING` -> `DEPLOYING` -> `READY` / `FAILED`.
- Call `deployxa_deployment_timeline` to check step milestones and durations.

### 4. Inspect Logs
- If the build is ongoing or has completed, call `deployxa_get_deployment_logs` with `deploymentId`.
- Present relevant log output concisely to the user, highlighting success or any build/runtime errors.
