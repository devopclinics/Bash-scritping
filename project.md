## System Administration Toolkit project

### Project Overview

The System Administration Toolkit is designed to streamline and automate essential system administration tasks through Bash scripting. The toolkit will include scripts for user management, log monitoring, disk usage reporting, and backup creation. Each script will encapsulate specific functionalities, ensuring modularity and maintainability.

### Project Objectives

- Automate common system administration tasks
- Improve efficiency and accuracy in user management
- Enhance log monitoring capabilities
- Ensure timely alerts for disk usage
- Provide reliable backup solutions

### Project Structure

```
sysadmin_toolkit/
├── backup.sh
├── check_disk_space.sh
├── log_monitor.sh
└── user_management.sh
```

### Script Descriptions

#### 1. User Management (`user_management.sh`)

**Purpose:** 
Manage system users, including creating, deleting, and listing users.

**Features:**
- Create a new user with a specified username and password.
- Delete an existing user.
- List all users on the system.

**Functions:**
- `create_user(username, password)`
- `delete_user(username)`
- `list_users()`

**Acceptance Criteria:**
- The script correctly creates a new user when provided with a username and password.
- The script successfully deletes an existing user.
- The script lists all current system users.

#### 2. Log Monitoring (`log_monitor.sh`)

**Purpose:**
Monitor specified log files for defined patterns and notify the administrator upon detection.

**Features:**
- Monitor a log file in real-time.
- Search for a specific pattern in the log file.
- Print lines that match the pattern.

**Functions:**
- `monitor_log(logfile, pattern)`

**Acceptance Criteria:**
- The script monitors the specified log file and prints lines matching the pattern.
- The script correctly handles log file updates in real-time.

#### 3. Disk Usage Reporting (`check_disk_space.sh`)

**Purpose:**
Monitor disk usage and send alerts when usage exceeds a specified threshold.

**Features:**
- Check disk usage of the root directory.
- Compare disk usage against a threshold.
- Send an email alert if the threshold is exceeded.

**Functions:**
- `check_disk_space()`

**Acceptance Criteria:**
- The script accurately checks the disk usage of the root directory.
- The script sends an alert if disk usage exceeds the specified threshold.

#### 4. Backup Creation (`backup.sh`)

**Purpose:**
Create backups of specified directories and store them in designated locations.

**Features:**
- Create a timestamped backup of a specified source directory.
- Store the backup in a specified destination directory.

**Functions:**
- `backup_directory(source, destination)`

**Acceptance Criteria:**
- The script creates a backup of the specified source directory.
- The backup is stored in the specified destination directory with a timestamped filename.

### Detailed Script Outlines

#### User Management (`user_management.sh`)

**Features to Implement:**
- Function to create a user
- Function to delete a user
- Function to list all users
- Main script logic to handle user input and call appropriate functions

#### Log Monitoring (`log_monitor.sh`)

**Features to Implement:**
- Function to monitor a log file for a specified pattern
- Main script logic to handle user input and call the monitor function

#### Disk Usage Reporting (`check_disk_space.sh`)

**Features to Implement:**
- Function to check disk usage
- Main script logic to call the check function

#### Backup Creation (`backup.sh`)

**Features to Implement:**
- Function to create a backup of a specified directory
- Main script logic to handle user input and call the backup function