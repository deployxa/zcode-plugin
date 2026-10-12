---
name: deployxa-diagnose
description: Diagnose failed or stuck deployments on Deployxa, explain operational anomalies using Engine evidence, and execute rollbacks.
---

# Deployxa Diagnosis & Incident Remediation Skill

This skill guides ZCode agents through troubleshooting failed deployments, identifying root causes, and executing remediation or rollbacks via Deployxa MCP tools.

## When to use this skill
- When a deployment status is `FAILED`, `CRASHED`, or stuck in `BUILDING`/`DEPLOYING`.
- When the user asks "Why is my deployment failing?" or "Why is it stuck?".
- When the user requests a rollback to a previously working deployment.

## Workflow

### 1. Identify Failed Deployment
- If `deploymentId` is not provided, call `deployxa_list_deployments` for the project to find the latest failed or active deployment.
- Call `deployxa_get_deployment` to check error codes and exit status.

### 2. Evidence-Based Root Cause Diagnosis
- Call `deployxa_diagnose_deployment` with `deploymentId` to run automated platform diagnostics.
- Call `deployxa_explain_deployment` with the user's specific question (e.g. "Why did the build step fail?").
  - *Important*: Do not guess causes from partial terminal text; always rely on the Engine's evidence-backed analysis.
- Call `deployxa_get_deployment_logs` to retrieve the relevant stack trace or compile error snippet.

### 3. Engine Assistant Consultation
- If further diagnostic depth is needed, invoke `deployxa_chat_assistant` with `projectId`, `deploymentId`, and a focused query.

### 4. Remediation & Rollback
- If the deployment failure is critical and production is affected:
  - Recommend rolling back to the last known healthy deployment.
  - Call `deployxa_rollback_deployment` with `deploymentId` (or `deployxa_rollback_workflow`).
- If configuration errors caused the issue (e.g. missing environment variable), guide the user using `deployxa-environment`.
