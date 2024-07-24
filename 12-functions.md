# Functions in Bash Scripting

## Introduction

Functions are an essential part of any programming language, including Bash scripting. They allow you to encapsulate a set of commands into a single unit, which can then be reused multiple times throughout your script. Functions improve code readability, maintainability, and reduce redundancy.

## Defining and Calling Functions

### Basic Syntax

The basic syntax for defining and calling a function in Bash is as follows:

```bash
function_name() {
    commands
}

# Call the function
function_name
```

### Example

#### Example 1: Basic Function

```bash
#!/bin/bash
# Description: Basic function example

greet() {
    echo "Hello, $1!"
}

# Call the function with an argument
greet "Alice"
```
- `greet() { ... }`: Defines a function named `greet`.
- `echo "Hello, $1!"`: Prints a greeting message. `$1` is the first argument passed to the function.
- `greet "Alice"`: Calls the `greet` function with the argument `"Alice"`.

## Function Parameters

Functions can accept parameters, allowing you to pass data to them. Parameters are accessed within the function using positional parameters `$1`, `$2`, etc.

### Example

#### Example 2: Function with Parameters

```bash
#!/bin/bash
# Description: Function with parameters

add() {
    local sum=$(( $1 + $2 ))
    echo "Sum: $sum"
}

# Call the function with arguments
add 5 3
```
- `add() { ... }`: Defines a function named `add`.
- `local sum=$(( $1 + $2 ))`: Calculates the sum of the first and second arguments and stores it in a local variable `sum`.
- `echo "Sum: $sum"`: Prints the sum.
- `add 5 3`: Calls the `add` function with arguments `5` and `3`.

## Returning Values from Functions

While functions cannot return values in the traditional sense, you can use `echo` to output a value and capture it using command substitution.

### Example

#### Example 3: Returning Values

```bash
#!/bin/bash
# Description: Function returning values

multiply() {
    local result=$(( $1 * $2 ))
    echo $result
}

# Capture the function's output
product=$(multiply 4 5)
echo "Product: $product"
```
- `multiply() { ... }`: Defines a function named `multiply`.
- `local result=$(( $1 * $2 ))`: Calculates the product of the first and second arguments and stores it in a local variable `result`.
- `echo $result`: Outputs the result.
- `product=$(multiply 4 5)`: Captures the function's output.
- `echo "Product: $product"`: Prints the product.

## Scope and Local Variables

By default, variables within functions are global. To limit the scope of a variable to the function, use the `local` keyword.

### Example

#### Example 4: Local Variables

```bash
#!/bin/bash
# Description: Function with local variables

increment() {
    local number=$1
    number=$(( number + 1 ))
    echo $number
}

# Global variable
number=10
echo "Original number: $number"

# Call the function
new_number=$(increment $number)
echo "Incremented number: $new_number"
echo "Global number remains: $number"
```
- `local number=$1`: Declares `number` as a local variable within the function.
- `number=10`: Sets a global variable `number`.
- `new_number=$(increment $number)`: Calls the `increment` function and captures its output.

## Functions with Default Parameters

You can set default values for parameters in functions to handle cases where arguments might not be provided.

### Example

#### Example 5: Default Parameters

```bash
#!/bin/bash
# Description: Function with default parameters

greet() {
    local name=${1:-Guest}
    echo "Hello, $name!"
}

# Call the function with and without arguments
greet "Alice"
greet
```
- `local name=${1:-Guest}`: Sets `name` to the first argument if provided; otherwise, defaults to "Guest".

## Nested Functions

Functions can call other functions within the script, enabling more complex workflows.

### Example

#### Example 6: Nested Functions

```bash
#!/bin/bash
# Description: Nested functions example

log_message() {
    echo "$(date): $1"
}

process_data() {
    local data=$1
    # Simulate processing
    sleep 1
    log_message "Processed data: $data"
}

# Call the function
process_data "Sample data"
```
- `log_message() { ... }`: Defines a function to log messages with a timestamp.
- `process_data() { ... }`: Defines a function to process data and log the result.
- `process_data "Sample data"`: Calls the `process_data` function with an argument.

## Real-Life Scenarios

### Scenario 1: Backup Script

A function can be used to create a backup of a directory.

#### Script: `backup.sh`

```bash
#!/bin/bash
# Description: Backup script

backup_directory() {
    local src=$1
    local dest=$2
    local timestamp=$(date +%Y%m%d%H%M%S)
    local backup_name=$(basename $src)_$timestamp.tar.gz

    tar -czf $dest/$backup_name $src
    echo "Backup of $src completed at $dest/$backup_name"
}

# Call the function
backup_directory "/path/to/source" "/path/to/destination"
```
- `backup_directory() { ... }`: Defines a function to create a backup.
- `tar -czf $dest/$backup_name $src`: Creates a compressed archive of the source directory.

### Scenario 2: User Management Script

A function can be used to create a new user and set a password.

#### Script: `user_management.sh`

```bash
#!/bin/bash
# Description: User management script

create_user() {
    local username=$1
    local password=$2

    useradd $username
    echo "$username:$password" | chpasswd
    echo "User $username created."
}

# Call the function
create_user "newuser" "password123"
```
- `create_user() { ... }`: Defines a function to create a user and set a password.
- `useradd $username`: Adds a new user.
- `echo "$username:$password" | chpasswd`: Sets the user's password.

### Scenario 3: Log Monitoring Script

A function can be used to monitor a log file for specific patterns.

#### Script: `log_monitor.sh`

```bash
#!/bin/bash
# Description: Log monitoring script

monitor_log() {
    local logfile=$1
    local pattern=$2

    tail -F $logfile | while read line; do
        if [[ $line =~ $pattern ]]; then
            echo "Pattern found: $line"
        fi
    done
}

# Call the function
monitor_log "/var/log/syslog" "ERROR"
```
- `monitor_log() { ... }`: Defines a function to monitor a log file.
- `tail -F $logfile`: Follows the log file for new entries.
- `if [[ $line =~ $pattern ]]; then`: Checks if the line matches the pattern.

