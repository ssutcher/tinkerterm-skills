---
name: asana
description: >
  Guide for managing tasks and projects in Asana. Use when the user asks to
  create tasks, search Asana, check project status, move tasks between sections,
  or comment on Asana tasks. Triggers on "asana", "asana task", "push to asana",
  "asana board", "asana project", "create task in asana".
---

# Asana

You have access to Asana through the tool library.

## Setup

If Asana isn't configured yet (execute_tool returns a settings error), walk the user through this:

**Required settings:**
- `asanaAccessToken` — Personal access token from app.asana.com/0/my-apps

**Configure with:**
```
configure_tool({ tool: "asana", setting: "asanaAccessToken", value: "<your-token>" })
```

After saving, verify with `execute_tool({ tool: "asana", action: "list_workspaces" })`.

The `asanaBaseUrl` setting has a working default and does not need to be configured.

## Common Workflows

### Discover workspace structure
Always start by discovering what the user has access to:
```
execute_tool({ tool: "asana", action: "list_workspaces" })
execute_tool({ tool: "asana", action: "list_projects", input: { workspace_gid: "..." } })
execute_tool({ tool: "asana", action: "list_sections", input: { project_gid: "..." } })
```

### Search for tasks
```
execute_tool({ tool: "asana", action: "search_tasks", input: {
  workspace_gid: "...",
  text: "login bug",
  completed: false,
  opt_fields: "name,assignee.name,due_on,completed,memberships.section.name"
}})
```
- Use `completed: false` to find only open tasks
- Filter by project: `projects.any: "project_gid"`
- Filter by assignee: `assignee.any: "user_gid"` or use `list_tasks` with `assignee: "me"`

### List tasks in a project or section
```
execute_tool({ tool: "asana", action: "list_tasks", input: {
  project: "...",
  completed_since: "now",
  opt_fields: "name,assignee.name,due_on,completed,memberships.section.name"
}})
```
- `completed_since: "now"` returns only incomplete tasks
- Use `section` instead of `project` to list tasks in a specific section

### Get task details
```
execute_tool({ tool: "asana", action: "get_task", input: { task_gid: "..." } })
```
Returns full task including notes, assignee, due date, projects, tags, and custom fields.

### View comments on a task
```
execute_tool({ tool: "asana", action: "get_task_stories", input: {
  task_gid: "...",
  opt_fields: "text,created_by.name,created_at,type"
}})
```
Stories include comments, status changes, and other events. Filter for `type: "comment"` in the results to show only comments.

### Create a task
1. First, discover the workspace and project GIDs if not already known
2. Then create (requires confirmation):
```
execute_tool({ tool: "asana", action: "create_task", input: {
  data: {
    name: "Fix login timeout bug",
    notes: "Users are getting logged out after 5 minutes...",
    workspace: "...",
    projects: ["..."],
    assignee: "me",
    due_on: "2026-01-15"
  }
}})
```
- Either `workspace` or `projects` is required (projects implies the workspace)
- `assignee` can be a user GID or `"me"` for the authenticated user

### Update a task
```
execute_tool({ tool: "asana", action: "update_task", input: {
  task_gid: "...",
  data: {
    completed: true
  }
}})
```
Only pass the fields you want to change. Common updates: `name`, `notes`, `assignee`, `due_on`, `completed`.

### Add a comment
```
execute_tool({ tool: "asana", action: "add_comment", input: {
  task_gid: "...",
  data: { text: "Investigated — root cause is the session timeout config." }
}})
```

### Move a task to a different section
1. First, list sections to find the target section GID:
```
execute_tool({ tool: "asana", action: "list_sections", input: { project_gid: "..." } })
```
2. Then move (requires confirmation):
```
execute_tool({ tool: "asana", action: "add_task_to_section", input: {
  section_gid: "...",
  data: { task: "task_gid" }
}})
```

## Response Formatting

- Show task lists as a table: name, assignee, due date, section, status
- Show GIDs alongside names when the user may need to reference them later
- For task details, format notes/description readably
- When listing projects or sections, include GIDs so follow-up actions are easy

## Important Rules

- Always call `list_workspaces` first if you don't know the workspace GID
- Always call `list_sections` before `add_task_to_section` — section GIDs are project-specific
- Always call `list_projects` before `create_task` if the project GID is uncertain
- `create_task`, `update_task`, `add_comment`, and `add_task_to_section` require user confirmation (confirm: true)
- Use `opt_fields` on read actions to get useful fields — Asana returns minimal data by default
- Good default opt_fields for tasks: `"name,completed,due_on,assignee.name,memberships.section.name"`
- Asana uses offset-based pagination — check `next_page` in responses for more results
- Dates are YYYY-MM-DD format for `due_on` and `start_on`
