---
description: Tools for interacting with the database
---

# Database Tools

Database tools provide functionality for interacting with the application's database, including managing scheduled tasks, retrieving DAO information, and searching for DAOs.

## Tool Overview

| Tool Name | Description | Key Features |
|-----------|-------------|--------------|
| `database_add_scheduled_task` | Add a new scheduled task | Cron scheduling, task naming |
| `database_list_scheduled_tasks` | List all scheduled tasks | Task details, status |
| `database_update_scheduled_task` | Update an existing scheduled task | Partial updates, enable/disable |
| `database_delete_scheduled_task` | Delete a scheduled task | Permanent removal |
| `database_get_dao_list` | Get a list of all DAOs | Token info, extension details |
| `database_get_dao_get_by_name` | Search for DAOs by various criteria | Flexible search, detailed results |

## Tool Details

### database_add_scheduled_task

Adds a new scheduled task to the database.

**Input Parameters**:
- `name`: Name of the scheduled task
- `prompt`: Prompt to schedule
- `cron`: Cron expression for the schedule (e.g., "0 0 * * *" for daily at midnight)

**Output**:
```json
{
  "id": "550e8400-e29b-41d4-a716-446655440000",
  "name": "Daily Bitcoin Price Check",
  "prompt": "Check the current Bitcoin price and report any significant changes",
  "cron": "0 0 * * *",
  "is_scheduled": true,
  "created_at": "2023-01-01T00:00:00Z"
}
```

**Example Prompt**:
```
Add a new scheduled task with the following details:
- name: Daily Bitcoin Price Check
- prompt: Check the current Bitcoin price and report any significant changes
- cron: 0 0 * * *
```

### database_list_scheduled_tasks

Lists all scheduled tasks for the current agent.

**Input Parameters**: None

**Output**:
```json
{
  "tasks": [
    {
      "id": "550e8400-e29b-41d4-a716-446655440000",
      "name": "Daily Bitcoin Price Check",
      "prompt": "Check the current Bitcoin price and report any significant changes",
      "cron": "0 0 * * *",
      "is_scheduled": true,
      "created_at": "2023-01-01T00:00:00Z",
      "last_run": "2023-01-02T00:00:00Z",
      "next_run": "2023-01-03T00:00:00Z"
    }
  ]
}
```

**Example Prompt**:
```
List all my scheduled tasks.
```

### database_update_scheduled_task

Updates an existing scheduled task in the database.

**Input Parameters**:
- `task_id`: ID of the scheduled task to update
- `name` (optional): New name for the scheduled task
- `prompt` (optional): New prompt for the task
- `cron` (optional): New cron expression for the schedule
- `enabled` (optional): Whether the schedule is enabled or not (true or false)

**Output**:
```json
{
  "id": "550e8400-e29b-41d4-a716-446655440000",
  "name": "Updated Bitcoin Price Check",
  "prompt": "Check the current Bitcoin price and report any significant changes",
  "cron": "0 12 * * *",
  "is_scheduled": true,
  "created_at": "2023-01-01T00:00:00Z",
  "updated_at": "2023-01-02T00:00:00Z"
}
```

**Example Prompt**:
```
Update an existing scheduled task with the following details:
- task_id: 550e8400-e29b-41d4-a716-446655440000
- name: Updated Bitcoin Price Check
- cron: 0 12 * * *
```

### database_delete_scheduled_task

Deletes a scheduled task from the database.

**Input Parameters**:
- `task_id`: ID of the scheduled task to delete

**Output**:
```json
{
  "success": true,
  "message": "Task deleted successfully"
}
```

**Example Prompt**:
```
Delete a scheduled task:
- task_id: 550e8400-e29b-41d4-a716-446655440000
```

### database_get_dao_list

Retrieves a list of all DAOs with their associated tokens.

**Input Parameters**: None

**Output**:
```json
{
  "dao_data": [
    {
      "dao": {
        "id": "550e8400-e29b-41d4-a716-446655440000",
        "name": "My DAO",
        "description": "A DAO for testing",
        "contract_id": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.my-dao",
        "created_at": "2023-01-01T00:00:00Z"
      },
      "token": {
        "id": "660e8400-e29b-41d4-a716-446655440000",
        "name": "My DAO Token",
        "symbol": "MDT",
        "contract_id": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.my-token",
        "dao_id": "550e8400-e29b-41d4-a716-446655440000"
      }
    }
  ]
}
```

**Example Prompt**:
```
Get a list of all DAOs with their associated tokens.
```

### database_get_dao_get_by_name

Searches for DAOs using multiple criteria.

**Input Parameters**:
- `name` (optional): Name or partial name of the DAO
- `description` (optional): Description text to search for
- `token_name` (optional): Name or partial name of the token
- `token_symbol` (optional): Symbol or partial symbol of the token
- `contract_id` (optional): Contract ID or partial contract ID

**Output**:
```json
{
  "matches": [
    {
      "dao": {
        "id": "550e8400-e29b-41d4-a716-446655440000",
        "name": "Bitcoin DAO",
        "description": "A DAO focused on Bitcoin",
        "contract_id": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.bitcoin-dao",
        "created_at": "2023-01-01T00:00:00Z"
      },
      "tokens": [
        {
          "id": "660e8400-e29b-41d4-a716-446655440000",
          "name": "Bitcoin DAO Token",
          "symbol": "BDT",
          "contract_id": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.bitcoin-token",
          "dao_id": "550e8400-e29b-41d4-a716-446655440000"
        }
      ],
      "extensions": [
        {
          "id": "770e8400-e29b-41d4-a716-446655440000",
          "name": "action-proposals",
          "contract_id": "ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.bitcoin-dao-action-proposals",
          "dao_id": "550e8400-e29b-41d4-a716-446655440000"
        }
      ]
    }
  ]
}
```

**Example Prompt**:
```
Search for DAOs with the following criteria:
- name: Bitcoin
```

## Error Handling

All database tools return standardized error responses when operations fail:

```json
{
  "success": false,
  "error": "Task not found",
  "code": 7001
}
```

Common error codes:
- 7001: Resource not found
- 7002: Invalid input
- 7003: Duplicate resource
- 7004: Database error
- 7005: Unauthorized access
