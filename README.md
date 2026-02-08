# Taskflow.nvim

Taskflow.nvim is a SQLite-backed task system for Neovim focused on fast capture, real dashboards, and repeatable workflows.

## Why

- Local, fast, and durable storage using SQLite
- One dashboard for active, backlog, completed, archived, and deleted tasks
- Recurring tasks that actually reschedule correctly
- Daily backups and optional email digests

## Install

### lazy.nvim

```lua
{
  "sminrana/nvim-taskflow",
  opts = {
    db_path = "~/Desktop/taskf/taskflow.db",
  },
}
```

### packer.nvim

```lua
use {
  "sminrana/nvim-taskflow",
  config = function()
    require("taskflow").setup({
      db_path = "~/Desktop/taskf/taskflow.db",
    })
  end,
}
```

## Configuration

```lua
require("taskflow").setup({
  db_path = "~/Desktop/taskf/taskflow.db",
  archive_after_days = 14,
  backup_dir = "~/Desktop/backup",
  backup_retain = 7,
  backup_time = { hour = 12, min = 0 },
  areas = { "general", "work", "personal" },
  rewards = {
    { threshold = 50, suggestion = "Take a long walk or coffee treat" },
    { threshold = 100, suggestion = "Buy a book or game" },
  },
})
```

## Commands

- `:TodoAdd`
- `:TodoList [important|today|next7|overdue|in_progress|completed|all]`
- `:TodoStart <id>`
- `:TodoComplete <id>`
- `:TodoStop <id>`
- `:TodoDashboard`
- `:TodoArea <area>`
- `:TodoWeeklyReview`
- `:TodoArchive [days]`
- `:TodoRewards`
- `:TodoRewardClaim <threshold>`
- `:TodoDelete <id>`
- `:TodoPostponeOverdue [days]`
- `:TodoDashboardHistory`
- `:TaskflowBackup`
- `:TaskflowBackupStart`
- `:TaskflowBackupStop`

## Keymaps

Default mappings:

- `<leader>jT` open dashboard
- `<leader>jta` add task
- `<leader>jte` send due email
- Visual `<leader>jtv` add task from selection

## Email Digest (optional)

Requires AWS SES via the AWS CLI.

Environment variables:

- `AWS_REGION`
- `TASKS_EMAIL_TO` (optional)

Enable on start:

```lua
require("taskflow").enable_auto_due_email_on_start()
```

## Data Location

The DB location is configurable via `db_path`. Default:

```
~/Desktop/taskf/taskflow.db
```

## License

MIT
