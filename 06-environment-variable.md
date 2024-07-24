# Environment Variables in Bash Scripting

## Introduction
Environment variables are predefined variables that are set in the system for each user. They store information about the system environment and the user session. These variables can be used in scripts to access system information and control processes.

## Checking Environment Variables

### 1. Using `env` Command
The `env` command lists all the environment variables and their values:
```bash
env
```

### 2. Using `printenv` Command
The `printenv` command also lists all the environment variables and their values:
```bash
printenv
```

### 3. Using `set` Command
The `set` command lists all the variables (including shell variables and environment variables) and their values:
```bash
set
```

### 4. Using `echo` Command
You can use the `echo` command to print the value of a specific environment variable. For example:
```bash
echo $HOME
echo $USER
echo $PATH
```

## Common Environment Variables
- `$HOME`: The home directory of the current user.
- `$USER`: The username of the current user.
- `$PATH`: The directories the shell searches for executable files.
- `$SHELL`: The path to the current shell.
- `$PWD`: The current working directory.
- `$LANG`: The current locale settings.
- `$MAIL`: The location of the current user's mail spool.
- `$LOGNAME`: The name of the current user.

## Creating an Environment Variable

To create an environment variable, use the following syntax:
```bash
export VarName=Value
```

### Example: Creating an Environment Variable
Let's create an environment variable called `TMPDIR` that will carry the `/tmp` directory path:
```bash
export TMPDIR=/tmp
```

- Check with `env` and you will see a new variable created:
    ```bash
    env | grep TMPDIR
    ```
- The variable will persist even after a system reboot.

### Unsetting an Environment Variable
To unset an environment variable, use the following command:
```bash
unset TMPDIR
```

- Check back in `env`: It is no longer there:
    ```bash
    env | grep TMPDIR
    ```

## Example 1: Displaying Environment Variables

### Script: `env.sh`
```bash
#!/bin/bash
# Description: Script to display environment variables

name=ami
echo "$name, Welcome to DevopsClinics"

echo "$name, find below your ENV variables"

echo "Your USER_ID is $SUDO_USER and you are running in $SHELL environment."
echo "You belong to USER $USER, GROUP $SUDO_GID and you are presently working in $PWD."
echo "You can find your mail in $MAIL and you can investigate the path below:"
echo "$PATH"
```

### Running the Script
1. **Create the script file:**
    ```bash
    touch env.sh
    ```

2. **Give execute permission to the file:**
    ```bash
    chmod +x env.sh
    ```

3. **Edit the script file:**
    ```bash
    vim env.sh
    ```

4. **Insert the complete script and save the file:**
    ```bash
    #!/bin/bash
    # Description: Script to display environment variables

    name=ami
    echo "$name, Welcome to DevopsClinics"

    echo "$name, find below your ENV variables"

    echo "Your USER_ID is $SUDO_USER and you are running in $SHELL environment."
    echo "You belong to USER $USER, GROUP $SUDO_GID and you are presently working in $PWD."
    echo "You can find your mail in $MAIL and you can investigate the path below:"
    echo "$PATH"
    ```
    - In `vim`, press `i` to insert the commands.
    - Save and quit `vim` by pressing `Esc` and typing `:wq`.

5. **Run the script:**
    ```bash
    ./env.sh
    ```

## Example 2: Using Environment Variables to Control Installation

### Script: `env2.sh`
```bash
#!/bin/bash
# Description: Script to install some packages
# Author: ami
# Date: May 2020

if [ "${USER}" != "root" ]
then
    echo "You need root access to run this"
    exit 1
fi

apt install finger -y
apt install curl -y
apt install zip -y
apt install vim -y
```

### Explanation
- The script checks if the current user is `root` using the `$USER` environment variable.
- If the user is not `root`, it prints a message and exits with an error code.
- If the user is `root`, it proceeds to install several packages using the `apt` package manager.

### Running the Script
1. **Create the script file:**
    ```bash
    touch env2.sh
    ```

2. **Give execute permission to the file:**
    ```bash
    chmod +x env2.sh
    ```

3. **Edit the script file:**
    ```bash
    vim env2.sh
    ```

4. **Insert the complete script and save the file:**
    ```bash
    #!/bin/bash
    # Description: Script to install some packages
    # Author: ami
    # Date: May 2020

    if [ "${USER}" != "root" ]
    then
        echo "You need root access to run this"
        exit 1
    fi

    apt install finger -y
    apt install curl -y
    apt install zip -y
    apt install vim -y
    ```
    - In `vim`, press `i` to insert the commands.
    - Save and quit `vim` by pressing `Esc` and typing `:wq`.

5. **Run the script:**
    ```bash
    sudo ./env2.sh
    ```

## Practical Live Scenarios of Using Environment Variables

### Scenario 1: Configuring Application Settings
Environment variables can be used to configure application settings without hardcoding them in the source code. For example, setting the database connection string:
```bash
export DB_HOST="localhost"
export DB_PORT="5432"
export DB_USER="admin"
export DB_PASS="secret"

./run_application.sh
```

### Scenario 2: Customizing User Environment
Users can customize their shell environment by setting environment variables in their `.bashrc` or `.bash_profile` files:
```bash
export EDITOR="vim"
export PATH="$PATH:/usr/local/bin"
```

### Scenario 3: Controlling Script Behavior
Environment variables can be used to control the behavior of scripts. For example, enabling debug mode in a script:
```bash
#!/bin/bash
# Description: Script with debug mode

if [ "$DEBUG" == "true" ]; then
    set -x
fi

echo "Running script..."

# Rest of the script
```

### Scenario 4: Passing Information to Child Processes
Environment variables can be used to pass information to child processes. For example, setting the `JAVA_HOME` variable for a Java application:
```bash
export JAVA_HOME="/usr/lib/jvm/java-11-openjdk"
./run_java_application.sh
```