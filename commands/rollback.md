# /rollback

Roll back a Deployxa project to a previous healthy deployment.

## Usage
`/rollback [deployment-id]`

## Instructions
1. Check the target deployment status with `deployxa_get_deployment`.
2. Confirm the target version or call `deployxa_rollback_deployment` with `{ deploymentId }`.
3. Report the newly created rollback deployment status and URL.
