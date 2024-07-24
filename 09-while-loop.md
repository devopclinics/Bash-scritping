
# The `while` Loop in Bash Scripting

## Introduction
The `while` loop enables you to execute a set of commands repeatedly until a specified condition occurs. It is usually used when you need to manipulate the value of a variable repeatedly. The `while` loop evaluates a condition, and if the condition is true, the given statements are executed. This process repeats until the condition evaluates to false.

## Basic Structure
The basic structure of a `while` loop in Bash is as follows:
```bash
while [ condition ]
do
    command1
    command2
    ...
    commandN
done
```

- `command1` to `commandN` will be executed repeatedly as long as the `condition` is true.
- The argument for a `while` loop can be any boolean expression.
- Infinite loops occur when the condition never evaluates to false.

### Example
```bash
#!/bin/bash
# Description: Basic while loop example

while [ 2 -eq 2 ]
do
    echo "This is a while loop"
    sleep 2
    echo "Success"
done
```
- `echo "This is a while loop"`: Prints the message "This is a while loop" to the terminal.
- `sleep 2`: Pauses the script for 2 seconds.
- `echo "Success"`: Prints the message "Success" to the terminal.

## Infinite `while` Loop
An infinite `while` loop is a loop that continues to execute indefinitely because the condition always evaluates to true.

### Example
```bash
#!/bin/bash
# Description: Infinite while loop example

while true
do
    echo "This is an infinite loop"
    sleep 2
done
```
- `while true`: Creates an infinite loop.
- `sleep 2`: Pauses the script for 2 seconds to prevent it from running too fast.

## Read a File Line By Line
The `while` loop can be used to read a file line by line. This is particularly useful for processing or analyzing large text files.

### Example
```bash
#!/bin/bash
# Description: Read a file line by line

filename="example.txt"
while read -r line
do
    echo "Line: $line"
done < "$filename"
```
- `filename="example.txt"`: Sets the file to be read.
- `while read -r line`: Reads the file line by line.
- `done < "$filename"`: Redirects the input to the `while` loop from the file.

## `break` and `continue` Statements
The `break` and `continue` statements are used to control the flow of loops in Bash scripting.

### `break` Statement
The `break` statement is used to exit the current loop before its natural termination.

#### Example
```bash
#!/bin/bash
# Description: Using break statement

n=1
while [ $n -le 10 ]
do
    if [ $n -eq 5 ]
    then
        break
    fi
    echo "$n"
    n=$(( n+1 ))
done
```
- `if [ $n -eq 5 ]`: Checks if `n` is equal to 5.
- `break`: Exits the loop when `n` equals 5.

### `continue` Statement
The `continue` statement is used to skip the current iteration of the loop and proceed to the next iteration.

#### Example
```bash
#!/bin/bash
# Description: Using continue statement

n=1
while [ $n -le 10 ]
do
    n=$(( n+1 ))
    if [ $n -eq 5 ]
    then
        continue
    fi
    echo "$n"
done
```
- `if [ $n -eq 5 ]`: Checks if `n` is equal to 5.
- `continue`: Skips the iteration when `n` equals 5.

## Practical Examples

### Real-Life Case Study 1: Monitoring System Resource Usage
**Scenario:** A system administrator needs to monitor the CPU usage of a server and log the usage every minute. If the CPU usage exceeds a threshold, an alert is triggered.

#### Script: `monitor_cpu.sh`
```bash
#!/bin/bash
# Description: Script to monitor CPU usage

THRESHOLD=80

while true
do
    CPU_USAGE=$(top -bn1 | grep "Cpu(s)" | sed "s/.*, *\([0-9.]*\)%* id.*/\1/" | awk '{print 100 - $1}')
    echo "Current CPU Usage: $CPU_USAGE%" >> cpu_usage.log

    if (( $(echo "$CPU_USAGE > $THRESHOLD" | bc -l) ))
    then
        echo "Alert: High CPU usage detected - $CPU_USAGE%" | mail -s "CPU Usage Alert" admin@example.com
    fi

    sleep 60
done
```
- `THRESHOLD=80`: Sets the CPU usage threshold to 80%.
- `while true`: Creates an infinite loop.
- `top -bn1`: Runs the `top` command in batch mode (`-b`) for one iteration (`-n1`).
- `grep "Cpu(s)"`: Filters the output to show lines containing "Cpu(s)".
- `sed "s/.*, *\([0-9.]*\)%* id.*/\1/"`: Uses `sed` to extract the CPU idle percentage.
- `awk '{print 100 - $1}'`: Uses `awk` to calculate the CPU usage percentage.
- `echo "Current CPU Usage: $CPU_USAGE%" >> cpu_usage.log`: Appends the CPU usage to `cpu_usage.log`.
- `if (( $(echo "$CPU_USAGE > $THRESHOLD" | bc -l) ))`: Checks if the CPU usage exceeds the threshold using `bc` for floating-point comparison.
- `mail -s "CPU Usage Alert" admin@example.com`: Sends an email alert.
- `sleep 60`: Pauses the script for 60 seconds.

### Real-Life Case Study 2: Backup Automation
**Scenario:** A system administrator needs to perform a backup of a directory every hour. The `while` loop is used to automate this process.

#### Script: `backup.sh`
```bash
#!/bin/bash
# Description: Script to automate directory backup

SOURCE_DIR="/path/to/source"
BACKUP_DIR="/path/to/backup"
while true
do
    rsync -av --delete $SOURCE_DIR $BACKUP_DIR
    echo "Backup performed at $(date)" >> backup.log
    sleep 3600
done
```
- `SOURCE_DIR="/path/to/source"`: Sets the source directory to be backed up.
- `BACKUP_DIR="/path/to/backup"`: Sets the backup directory.
- `while true`: Creates an infinite loop.
- `rsync -av --delete $SOURCE_DIR $BACKUP_DIR`: Uses `rsync` to synchronize the source and backup directories with archive mode (`-a`), verbose output (`-v`), and deletion of files not present in the source (`--delete`).
- `echo "Backup performed at $(date)" >> backup.log`: Logs the backup operation with a timestamp.
- `sleep 3600`: Pauses the script for 3600 seconds (1 hour).

### Real-Life Case Study 3: User Input Validation
**Scenario:** A script requires the user to input a valid number. The `while` loop ensures the input meets the required conditions before proceeding.

#### Script: `validate_input.sh`
```bash
#!/bin/bash
# Description: Script to validate user input

while true
do
    echo "Please enter a number between 1 and 10:"
    read number

    if [[ "$number" =~ ^[1-9]$|^10$ ]]
    then
        echo "Valid input: $number"
        break
    else
        echo "Invalid input. Try again."
    fi
done
```
- `while true`: Creates an infinite loop.
- `echo "Please enter a number between 1 and 10:"`: Prompts the user for input.
- `read number`: Reads the user input into the variable `number`.
- `if [[ "$number" =~ ^[1-9]$|^10$ ]]`: Uses a regular expression to check if the input is a number between 1 and 10.
- `break`: Exits the loop if the input is valid.
- `else echo "Invalid input. Try again."`: Prompts the user to try again if the input is invalid.

### Example: Printing Multiplication Table
**Scenario:** A script to print the multiplication table of a given number.

#### Script: `multiplication_table.sh`
```bash
#!/bin/bash
# Description: Script to print multiplication table of a given number
# Version: 1.0
# Date: 07/28/2021

echo "What is your value: "
read value
i=1
while [ $i -le 10 ]
do
    result=$((value * i))
    echo "$value * $i = $result"
    i=$((i+1))
done
```
- `echo "What is your value: "`: Prompts the user to enter a number.
- `read value`: Reads the user input into the variable `value`.
- `i=1`: Initializes the variable `i` to 1.
- `while [ $i -le 10 ]`: Continues the loop as long as `i` is less than or equal to 10

.
- `result=$((value * i))`: Calculates the product of `value` and `i`.
- `echo "$value * $i = $result"`: Prints the multiplication result to the terminal.
- `i=$((i+1))`: Increments `i` by 1.

