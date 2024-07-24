# Read Statement in Bash Scripting

## Introduction
The `read` command is a built-in Bash command that reads the contents of a line into a variable. It allows for word splitting that is tied to the special shell variable `IFS` (Internal Field Separator). It is primarily used for catching user input but can also be used to implement functions that take input from standard input.

## Basic Syntax
The basic syntax of the `read` command in Bash is as follows:
```bash
read variable_name
```
- `variable_name`: The name of the variable into which the input will be read.

## Example: Using the Read Statement

### Script: `read.sh`
```bash
#!/bin/bash
# Description: Testing the read command
# Date: 07272021

echo "YOU ARE WELCOME TO DEVOPSCLINICS"
echo "What is your name?"
read name

if [ -z "${name}" ]
then
    echo "Please enter your name"
else
    echo "What is your date of birth?"
    read dob
    if [ -z "${dob}" ]
    then
        echo "$name, your date of birth is required before you can proceed"
    else
        echo "What is your sex?"
        read sex
        if [ -z "${sex}" ]
        then
            echo "$name, please enter either Male or Female"
        else
            echo "Why are you here?"
            read reason
            if [ -z "${reason}" ]
            then
                echo "We need to know why you are here, $name"
            else
                echo "Hello ${name}, you are a ${sex} and your date of birth is ${dob}."
                echo "You are here because: ${reason}"
            fi
        fi
    fi
fi
```

### Explanation
1. The script welcomes the user and prompts for their name.
2. It reads the user's name into the `name` variable.
3. If the name is not provided, it prompts the user to enter their name.
4. If the name is provided, it prompts for the date of birth (`dob`).
5. If the date of birth is not provided, it notifies the user that it is required.
6. If the date of birth is provided, it prompts for the user's sex (`sex`).
7. If the sex is not provided, it asks the user to enter either "Male" or "Female".
8. If the sex is provided, it prompts for the reason why the user is here (`reason`).
9. If the reason is not provided, it asks the user to specify the reason.
10. If all inputs are provided, it displays a summary message including the name, sex, date of birth, and reason.

### Running the Script
1. **Create the script file:**
    ```bash
    touch read.sh
    ```

2. **Give execute permission to the file:**
    ```bash
    chmod +x read.sh
    ```

3. **Edit the script file:**
    ```bash
    vim read.sh
    ```

4. **Insert the complete script and save the file:**
    ```bash
    #!/bin/bash
    # Description: Testing the read command
    # Date: 07272021

    echo "YOU ARE WELCOME TO DEVOPSCLINICS"
    echo "What is your name?"
    read name

    if [ -z "${name}" ]
    then
        echo "Please enter your name"
    else
        echo "What is your date of birth?"
        read dob
        if [ -z "${dob}" ]
        then
            echo "$name, your date of birth is required before you can proceed"
        else
            echo "What is your sex?"
            read sex
            if [ -z "${sex}" ]
            then
                echo "$name, please enter either Male or Female"
            else
                echo "Why are you here?"
                read reason
                if [ -z "${reason}" ]
                then
                    echo "We need to know why you are here, $name"
                else
                    echo "Hello ${name}, you are a ${sex} and your date of birth is ${dob}."
                    echo "You are here because: ${reason}"
                fi
            fi
        fi
    fi
    ```
    - In `vim`, press `i` to insert the commands.
    - Save and quit `vim` by pressing `Esc` and typing `:wq`.

5. **Run the script:**
    ```bash
    ./read.sh
    ```