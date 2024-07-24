
# Exit Codes and Command Substitution in Bash Scripting

## Introduction

In Bash scripting, exit codes and command substitution are essential concepts. Exit codes are used to determine the success or failure of a command, while command substitution allows you to capture the output of a command and use it as part of another command or variable.

## Exit Codes

### What are Exit Codes?

Exit codes are numeric values returned by a command to indicate its success or failure. By convention, an exit code of `0` indicates success, while any non-zero value indicates an error.

### Checking Exit Codes

You can check the exit code of the last executed command using the special variable `$?`.

### Checking Exit Codes on the CLI

To check the exit code of a command directly on the command line, you can follow these steps:

1. Execute a command:
    ```bash
    ls /nonexistent_directory
    ```

2. Immediately check the exit code of the last command:
    ```bash
    echo $?
    ```

3. If the command was successful, the exit code will be `0`. If it failed, you will see a non-zero exit code.

### Example

```bash
#!/bin/bash
# Description: Example of using exit codes

mkdir /tmp/test_directory
if [ $? -eq 0 ]; then
    echo "Directory created successfully."
else
    echo "Failed to create directory."
fi
```
- `mkdir /tmp/test_directory`: Creates a directory.
- `if [ $? -eq 0 ]`: Checks if the exit code of the previous command is `0`.
- `echo "Directory created successfully."`: Prints success message.
- `echo "Failed to create directory."`: Prints failure message if the exit code is not `0`.

### Practical Example: Checking Command Success

#### Script: `check_command.sh`

```bash
#!/bin/bash
# Description: Script to check if a command succeeds

ping -c 1 google.com
if [ $? -eq 0 ]; then
    echo "Internet connection is available."
else
    echo "No internet connection."
fi
```
- `ping -c 1 google.com`: Sends one ping to `google.com`.
- `if [ $? -eq 0 ]`: Checks if the ping command was successful.
- `echo "Internet connection is available."`: Prints success message if the exit code is `0`.
- `echo "No internet connection."`: Prints failure message if the exit code is not `0`.

## Command Substitution

### What is Command Substitution?

Command substitution allows you to capture the output of a command and use it as part of another command or assign it to a variable. It is done using backticks (\`\`) or the `$(command)` syntax.

### Syntax

```bash
variable=$(command)
# or using backticks
variable=`command`
```

### Example

```bash
#!/bin/bash
# Description: Example of command substitution

current_date=$(date)
echo "Current date and time: $current_date"
```
- `current_date=$(date)`: Captures the output of the `date` command into the `current_date` variable.
- `echo "Current date and time: $current_date"`: Prints the current date and time.

### Practical Example: Capturing Command Output

#### Script: `list_files.sh`

```bash
#!/bin/bash
# Description: Script to list files and store in a variable

file_list=$(ls -1)
echo "Files in the current directory:"
echo "$file_list"
```
- `file_list=$(ls -1)`: Captures the list of files in the current directory.
- `echo "Files in the current directory:"`: Prints a message.
- `echo "$file_list"`: Prints the list of files.

## Combining Exit Codes and Command Substitution

### Example: Checking Command Success and Capturing Output

#### Script: `check_and_capture.sh`

```bash
#!/bin/bash
# Description: Script to check command success and capture output

output=$(ping -c 1 google.com)
exit_code=$?

if [ $exit_code -eq 0 ]; then
    echo "Ping successful. Output:"
    echo "$output"
else
    echo "Ping failed with exit code $exit_code."
fi
```
- `output=$(ping -c 1 google.com)`: Captures the output of the `ping` command.
- `exit_code=$?`: Captures the exit code of the `ping` command.
- `if [ $exit_code -eq 0 ]`: Checks if the exit code is `0`.
- `echo "Ping successful. Output:"`: Prints success message if the exit code is `0`.
- `echo "$output"`: Prints the output of the `ping` command.
- `echo "Ping failed with exit code $exit_code."`: Prints failure message if the exit code is not `0`.

## Real-Life Case Study: Automation Script

**Scenario:** An automation script that checks disk space and sends an alert if the usage exceeds a threshold.

#### Script: `check_disk_space.sh`

```bash
#!/bin/bash
# Description: Script to check disk space and send an alert

THRESHOLD=80
disk_usage=$(df / | grep / | awk '{ print $5 }' | sed 's/%//g')
exit_code=$?

if [ $exit_code -ne 0 ]; then
    echo "Failed to get disk usage."
    exit $exit_code
fi

if [ $disk_usage -ge $THRESHOLD ]; then
    echo "Disk usage is above $THRESHOLD%. Current usage is $disk_usage%."
    # Send an alert (e.g., email)
    echo "Alert: Disk usage is $disk_usage%" | mail -s "Disk Usage Alert" admin@example.com
else
    echo "Disk usage is below $THRESHOLD%. Current usage is $disk_usage%."
fi
```
- `THRESHOLD=80`: Sets the disk usage threshold to 80%.
- `disk_usage=$(df / | grep / | awk '{ print $5 }' | sed 's/%//g')`: Captures the disk usage percentage.
- `exit_code=$?`: Captures the exit code of the `df` command.
- `if [ $exit_code -ne 0 ]`: Checks if the exit code is not `0`.
- `echo "Failed to get disk usage."`: Prints failure message.
- `exit $exit_code`: Exits the script with the captured exit code.
- `if [ $disk_usage -ge $THRESHOLD ]`: Checks if the disk usage exceeds the threshold.
- `echo "Disk usage is above $THRESHOLD%. Current usage is $disk_usage%."`: Prints alert message.
- `echo "Alert: Disk usage is $disk_usage%" | mail -s "Disk Usage Alert" admin@example.com`: Sends an email alert.
- `echo "Disk usage is below $THRESHOLD%. Current usage is $disk_usage%."`: Prints normal usage message.

