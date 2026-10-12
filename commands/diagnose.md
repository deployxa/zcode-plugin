# /diagnose

Diagnose a stuck or failed Deployxa deployment using Engine evidence.

## Usage
`/diagnose [deployment-id]`

## Instructions
1. If `deployment-id` is omitted, list recent deployments using `deployxa_list_all_deployments` and pick the most recent failed/active deployment.
2. Call `deployxa_diagnose_deployment` with `{ deploymentId }`.
3. Call `deployxa_explain_deployment` with `{ deploymentId, question: "Why did this deployment fail or get stuck?" }`.
4. Summarize the root cause, failing step, and safe recommended actions (such as config fixes or rollback).
