# /deploy

Trigger a new deployment for a Deployxa project.

## Usage
`/deploy [project-id] [branch]`

## Instructions
1. If `project-id` is omitted, call `deployxa_list_projects` to determine the project matching the current repository directory.
2. If `branch` is omitted, default to the current active Git branch.
3. Call `deployxa_create_deployment` with `{ projectId, branch }`.
4. Poll `deployxa_deployment_progress` until completion or stream the initial logs using `deployxa_get_deployment_logs`.
5. Report the final deployment URL and status.
