# Bash Scripting: Using Cron Jobs

## Introduction to Cron Jobs

Cron is a time-based job scheduler in Unix-like operating systems. It allows users to schedule scripts or commands to run automatically at specified intervals. This can be especially useful for automating repetitive tasks with bash scripts, such as backups, system maintenance, or sending periodic notifications.

## Cron Job Basics

### The Cron Table (crontab)

The `crontab` is a file that contains the schedule of cron entries to be run and their corresponding shell commands. Each user on a Unix-like system can have their own crontab. The cron daemon reads these files and executes the scheduled tasks at the specified times.

### Crontab Syntax

A crontab file consists of lines with six fields each. The fields specify the time and date for the command's execution, followed by the command itself. Here's a breakdown of the fields:

```
*     *     *     *     *  command to be executed
-     -     -     -     -
|     |     |     |     |
|     |     |     |     +----- Day of the week (0 - 7) (Sunday = 0 or 7)
|     |     |     +------- Month (1 - 12)
|     |     +--------- Day of the month (1 - 31)
|     +----------- Hour (0 - 23)
+------------- Minute (0 - 59)
```

- **Minute**: Specifies the minute of the hour when the command will run (0-59).
- **Hour**: Specifies the hour of the day when the command will run (0-23).
- **Day of the month**: Specifies the day of the month when the command will run (1-31).
- **Month**: Specifies the month when the command will run (1-12).
- **Day of the week**: Specifies the day of the week when the command will run (0-7, where both 0 and 7 represent Sunday).

For example, a line in the crontab file like `30 14 * * 5 /path/to/command` means "run `/path/to/command` at 2:30 PM every Friday".

### Special Strings

Cron also accepts several special strings that can be used in place of the five time-and-date fields:

- `@reboot` - Run once, at startup.
- `@yearly` or `@annually` - Run once a year, equivalent to `0 0 1 1 *`.
- `@monthly` - Run once a month, equivalent to `0 0 1 * *`.
- `@weekly` - Run once a week, equivalent to `0 0 * * 0`.
- `@daily` or `@midnight` - Run once a day, equivalent to `0 0 * * *`.
- `@hourly` - Run once an hour, equivalent to `0 * * * *`.

## Managing Crontabs

### Viewing the Crontab

To view the current user's crontab, use:

```sh
crontab -l
```

This command displays all the cron jobs scheduled for the current user. It's useful for checking existing schedules and ensuring your tasks are set up correctly.

### Editing the Crontab

To edit the current user's crontab, use:

```sh
crontab -e
```

This command opens the crontab file in the default text editor. Here, you can add, modify, or remove cron jobs. Each line in the file represents a scheduled task.

### Removing the Crontab

To remove the current user's crontab, use:

```sh
crontab -r
```

This command deletes all the scheduled tasks for the current user. Use it with caution, as it removes all entries without prompting for confirmation.

## Creating Cron Jobs with Bash Scripts

### Example 1: Running a Script Every Minute

1. **Create the Bash Script**:

    Create a file named `example1.sh`:

    ```sh
    #!/bin/bash
    # Description: A script to log the current time
    echo "Current time: $(date)" >> /path/to/logfile.log
    ```

    This script logs the current date and time to a specified log file every time it runs.

    Make the script executable:

    ```sh
    chmod +x example1.sh
    ```

2. **Schedule the Cron Job**:

    Edit the crontab:

    ```sh
    crontab -e
    ```

    Add the following line to run the script every minute:

    ```sh
    * * * * * /path/to/example1.sh
    ```

    This entry tells cron to execute `example1.sh` every minute, logging the current time continuously.

### Example 2: Running a Backup Script Daily

1. **Create the Bash Script**:

    Create a file named `backup.sh`:

    ```sh
    #!/bin/bash
    # Description: A script to back up a directory
    tar -czf /path/to/backup/$(date +\%Y-\%m-\%d).tar.gz /path/to/directory
    ```

    This script creates a compressed archive of a specified directory, with the filename based on the current date.

    Make the script executable:

    ```sh
    chmod +x backup.sh
    ```

2. **Schedule the Cron Job**:

    Edit the crontab:

    ```sh
    crontab -e
    ```

    Add the following line to run the script daily at 2 AM:

    ```sh
    0 2 * * * /path/to/backup.sh
    ```

    This entry schedules the `backup.sh` script to run every day at 2 AM, ensuring regular backups.

### Example 3: Running a Script at System Reboot

1. **Create the Bash Script**:

    Create a file named `reboot_script.sh`:

    ```sh
    #!/bin/bash
    # Description: A script to run at system reboot
    echo "System rebooted at: $(date)" >> /path/to/reboot.log
    ```

    This script logs the system reboot time to a specified log file.

    Make the script executable:

    ```sh
    chmod +x reboot_script.sh
    ```

2. **Schedule the Cron Job**:

    Edit the crontab:

    ```sh
    crontab -e
    ```

    Add the following line to run the script at system reboot:

    ```sh
    @reboot /path/to/reboot_script.sh
    ```

    This entry schedules the `reboot_script.sh` to run every time the system boots up, logging the reboot event.

## Best Practices for Using Cron Jobs

1. **Absolute Paths**:
   - Always use absolute paths for scripts and files to avoid issues with relative paths. This ensures the script can locate all necessary files and directories regardless of the current working directory.

2. **Environment Variables**:
   - Cron jobs run in a limited environment. Make sure to set any necessary environment variables within the script. For example, set the PATH variable if the script relies on non-standard locations for executables.

3. **Logging**:
   - Log the output of cron jobs for troubleshooting. Use `>>` to append output to a log file. For example, `script.sh >> /path/to/logfile.log 2>&1` captures both standard output and errors.

4. **Permissions**:
   - Ensure that the scripts have the correct permissions to execute and access the required files and directories. The script and all referenced files should be readable and executable by the user running the cron job.

5. **Test Scripts Manually**:
   - Before scheduling a script with cron, test it manually to ensure it works as expected. This helps identify and fix issues before automation.

## Conclusion

Cron jobs are a powerful tool for automating tasks in Unix-like systems. By combining cron with bash scripts, you can automate a wide range of tasks, from simple time logging to complex backup operations. Understanding and using cron effectively can greatly enhance your productivity and ensure that repetitive tasks are handled efficiently.