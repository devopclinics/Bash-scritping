
# Bash Scripting: `awk` and `sed` Commands

## Introduction

In Bash scripting, `awk` and `sed` are essential tools for text processing. `awk` is used for pattern scanning and processing, while `sed` is a stream editor for filtering and transforming text. This tutorial will guide you from simple to complex examples, including real-life scenarios.

## `awk` Command

### What is `awk`?

`awk` is a programming language designed for text processing and typically used as a data extraction and reporting tool. It allows you to scan a file line by line, split each line into fields, compare the fields to patterns, and perform actions on matching lines.

### Basic Syntax

```bash
awk 'pattern { action }' filename
```

- `pattern`: The pattern to search for in the file.
- `action`: The action to perform when the pattern matches.
- `filename`: The name of the file to process.

### Simple Examples

#### Example 1: Print Entire File

```bash
awk '{ print }' file.txt
```

- `{ print }`: Prints each line of the file.

#### Example 2: Print Specific Field

```bash
awk '{ print $1 }' file.txt
```

- `{ print $1 }`: Prints the first field of each line.

### Field Separator

#### Example 3: Using Custom Field Separator

```bash
awk -F, '{ print $1 }' file.csv
```

- `-F,`: Sets the field separator to a comma.
- `{ print $1 }`: Prints the first field of each line.

### Conditional Statements

#### Example 4: Print Lines Matching a Pattern

```bash
awk '/pattern/ { print }' file.txt
```

- `/pattern/ { print }`: Prints lines containing the pattern.

#### Example 5: Print Specific Field for Matching Lines

```bash
awk '/pattern/ { print $2 }' file.txt
```

- `/pattern/ { print $2 }`: Prints the second field of lines containing the pattern.

### Complex Examples

#### Example 6: Calculate Sum of a Column

```bash
awk '{ sum += $1 } END { print sum }' file.txt
```

- `{ sum += $1 }`: Adds the value of the first field to the variable `sum`.
- `END { print sum }`: Prints the value of `sum` after processing all lines.

### Real-Life Scenarios

#### Scenario 1: Extracting Usernames from `/etc/passwd`

```bash
awk -F: '{ print $1 }' /etc/passwd
```

- `-F:`: Sets the field separator to a colon.
- `{ print $1 }`: Prints the first field (username) of each line.

#### Scenario 2: Generating a Report from a Log File

```bash
awk '$9 == 404 { print $1, $4, $7 }' access.log > 404_report.txt
```

- `$9 == 404 { print $1, $4, $7 }`: Prints the IP address, timestamp, and requested URL for lines where the status code is 404.
- `> 404_report.txt`: Redirects the output to `404_report.txt`.

## `sed` Command

### What is `sed`?

`sed` (stream editor) is a non-interactive command-line text editor. It is used to perform basic text transformations on an input stream (a file or input from a pipeline).

### Basic Syntax

```bash
sed 's/pattern/replacement/' filename
```

- `s/pattern/replacement/`: Substitutes the first occurrence of `pattern` with `replacement` in each line.
- `filename`: The name of the file to process.

### Simple Examples

#### Example 1: Replace First Occurrence of a Pattern

```bash
sed 's/old/new/' file.txt
```

- `s/old/new/`: Replaces the first occurrence of `old` with `new` in each line.

#### Example 2: Replace All Occurrences of a Pattern

```bash
sed 's/old/new/g' file.txt
```

- `s/old/new/g`: Replaces all occurrences of `old` with `new` in each line.

### Using Delimiters

#### Example 3: Using Custom Delimiter

```bash
sed 's|/usr/bin|/usr/local/bin|g' file.txt
```

- `s|/usr/bin|/usr/local/bin|g`: Uses `|` as the delimiter instead of `/`.

### Deleting Lines

#### Example 4: Delete Specific Line

```bash
sed '3d' file.txt
```

- `3d`: Deletes the third line of the file.

#### Example 5: Delete Lines Matching a Pattern

```bash
sed '/pattern/d' file.txt
```

- `/pattern/d`: Deletes lines containing the pattern.

### Complex Examples

#### Example 6: Insert Line Before a Pattern

```bash
sed '/pattern/i\This is a new line' file.txt
```

- `/pattern/i\This is a new line`: Inserts `This is a new line` before lines containing the pattern.

#### Example 7: Append Line After a Pattern

```bash
sed '/pattern/a\This is a new line' file.txt
```

- `/pattern/a\This is a new line`: Appends `This is a new line` after lines containing the pattern.

### Real-Life Scenarios

#### Scenario 1: Modify Configuration Files

```bash
sed -i 's/^#\(.*option\)/\1/' config.cfg
```

- `-i`: Edits the file in place.
- `s/^#\(.*option\)/\1/`: Uncomments lines containing `option`.

#### Scenario 2: Batch Rename Files

```bash
for file in *.txt; do
    newname=$(echo $file | sed 's/old/new/')
    mv "$file" "$newname"
done
```

- `for file in *.txt`: Loops through all `.txt` files.
- `newname=$(echo $file | sed 's/old/new/')`: Uses `sed` to generate the new file name.
- `mv "$file" "$newname"`: Renames the file.

## Combining `awk` and `sed`

### Example: Data Cleaning

```bash
awk '{ print $1, $2 }' file.txt | sed 's/old/new/g'
```

- `awk '{ print $1, $2 }' file.txt`: Extracts the first and second fields from `file.txt`.
- `sed 's/old/new/g'`: Replaces all occurrences of `old` with `new` in the output from `awk`.

### Real-Life Case Study: Log File Analysis

**Scenario:** Extract IP addresses from a log file, count occurrences, and replace dots with underscores.

#### Script: `log_analysis.sh`

```bash
#!/bin/bash
# Description: Script to analyze log files

awk '{ print $1 }' access.log | sort | uniq -c | sort -nr | sed 's/\./_/g' > ip_report.txt
```
- `awk '{ print $1 }' access.log`: Extracts the IP addresses from `access.log`.
- `sort`: Sorts the IP addresses.
- `uniq -c`: Counts the occurrences of each IP address.
- `sort -nr`: Sorts the counts in descending order.
- `sed 's/\./_/g'`: Replaces dots with underscores in the IP addresses.
- `> ip_report.txt`: Redirects the output to `ip_report.txt`.
