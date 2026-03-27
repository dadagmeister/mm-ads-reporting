# CLAUDE.md — MM Paid Monitoring

## Project
n8n workflow for MindMeister (MM) Google Ads monitoring. See SPEC.md for full details.

## Workflow File
`workflow.json` is the n8n workflow. To update the workflow in n8n:
1. Edit `workflow.json`
2. Delete the existing workflow in n8n (per workaround below)
3. Import `workflow.json` via n8n MCP `create_workflow`

## n8n Update Workaround
`update_workflow` always fails. Always use **delete + create** to update a workflow:
```
1. mcp__n8n-local__delete_workflow(workflowId)
2. mcp__n8n-local__create_workflow(name, nodes, connections)
```

## Key IDs
- **Workflow ID**: `anZ9xDsVR1jabmE5`
- **MM Sheet**: `1Uag5Qd7elO6R6S1VLXvWIATfK9MHHbNkr-sNM1BOaX0`
- **Budget Sheet**: `1u_AiGmpo27x5nGQrhTj91uUez6fYWkhSBjx3k_CIw2I`
- **Slack test channel**: `C08NX15CMEJ`

## Branching
- `main` — stable
- `daan` — Daan's working branch
- `mark` — Mark's working branch
