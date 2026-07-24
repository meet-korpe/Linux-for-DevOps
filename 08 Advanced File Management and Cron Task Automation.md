# 8. Advanced File Management and Cron Task Automation

These notes focuses on advanced file copying techniques and the automation of tasks using the **Cron** utility.

## 1. Advanced Copy (cp) Operations

Building on basic file management, these commands provide more control over how files and directories are copied.

- **Copying Multiple Items**: You can copy several files into a single destination directory in one command.
  - Example: `cp file1 file2 file3 /dir6/`
- **Preserving Metadata (-p)**: This flag ensures that the **permissions, ownership, and timestamps** of the original file are preserved in the copy.
  - Example: `cp -p file3 file5`
- **Using Wildcards**: Wildcards allow you to copy groups of files based on patterns.
  - **All files**: `cp /data/* /backup/` copies every file in the directory.
  - **Specific extensions**: `cp *.txt /backup/` copies only text files; `cp *.log /backup/` copies only log files.
  - **Hidden files**: `cp -r .* /backup/` specifically targets and copies hidden files and directories.

## 2. Task Scheduling with Cron

**Cron** is a time-based job scheduler in Linux used to run scripts or commands automatically at specific intervals.

### A. Managing the Cron Service

- **crond**: The background daemon (service) that executes scheduled tasks.
- **Service Commands (CentOS 6)**:
  - `service crond start`: Starts the cron service.
  - `service crond status`: Checks if the service is currently running.

### B. The crontab Command

The crontab (cron table) command is used to manage your list of scheduled jobs.

- `crontab -e`: **Edit** your crontab to add or change jobs.
- `crontab -l`: **List** all currently scheduled jobs.
- `crontab -r`: **Remove** or delete your entire crontab.

### C. Crontab Syntax and Format

A cron entry consists of five time fields followed by the command to be executed. The format is: **minute hour day_of_month month day_of_week command**.

| Field | Range | Description |
| :--- | :--- | :--- |
| Minute | 0 - 59 | Exact minute the job runs |
| Hour | 0 - 23 | Hour of the day (24-hour format) |
| Day of Month | 1 - 31 | Specific day of the month |
| Month | 1 - 12 | Month of the year |
| Day of Week | 0 - 7 | 0 and 7 both represent Sunday |

### D. Scheduling Examples

- **Every minute**: `* * * * * [command]`
- **Every 5 minutes**: `*/5 * * * * [command]`
- **Every hour (at the top of the hour)**: `0 * * * * [command]`
- **Daily at 2:00 AM**: `0 2 * * * [command]`
- **Daily at 6:30 PM**: `30 18 * * * [command]`
- **Every Sunday at 10:00 PM**: `0 22 * * 0 [command]`
- **First day of every month at midnight**: `0 0 1 * * [command]`
- **Every year on January 1st at midnight**: `0 0 1 1 * [command]`

