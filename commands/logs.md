# /logs

Inspect bounded build and runtime logs for a Deployxa deployment.

## Usage
`/logs [deployment-id]`

## Instructions
1. If `deployment-id` is omitted, query `deployxa_list_all_deployments` to find the latest deployment.
2. Call `deployxa_get_deployment_logs` with `{ deploymentId }`.
3. Output the bounded log output with any secret values redacted.
