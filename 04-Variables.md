# Variables in Scripting

## Introduction
A variable in scripting is a placeholder for storing data values. It allows you to assign values and reference them throughout your script.

## Setting a Value for a Variable
To set a value for a variable, use the following syntax:
```bash
VariableName=VariableValue
```
Example:
```bash
greeting="Hello, World!"
```

## Reading the Value of a Variable
To read the value of a variable, use the `$` symbol followed by the variable name or enclose the variable name in curly braces:
```bash
$VariableName
${VariableName}
```
Example:
```bash
$greeting
${greeting}
```

## Example of Single Variable Declaration

### Script: `single_variable.sh`
```bash
#!/bin/bash
# Description: Example of single variable declaration

NAME="Alice"
echo "$NAME is learning Bash scripting."
echo "$NAME finds it very interesting."
echo "$NAME is practicing daily to improve."
echo "$NAME will soon master Bash scripting."
```

### Running the Script
1. **Create the script file:**
    ```bash
    touch single_variable.sh
    ```

2. **Give execute permission to the file:**
    ```bash
    chmod +x single_variable.sh
    ```

3. **Edit the script file:**
    ```bash
    vim single_variable.sh
    ```

4. **Insert the script and save the file:**
    ```bash
    #!/bin/bash
    # Description: Example of single variable declaration

    NAME="Alice"
    echo "$NAME is learning Bash scripting."
    echo "$NAME finds it very interesting."
    echo "$NAME is practicing daily to improve."
    echo "$NAME will soon master Bash scripting."
    ```
    - In `vim`, press `i` to insert the commands.
    - Save and quit `vim` by pressing `Esc` and typing `:wq`.

5. **Run the script:**
    ```bash
    ./single_variable.sh
    ```

## Example of Multiple Variable Declarations

### Script: `multiple_variables.sh`
```bash
#!/bin/bash
# Description: Example of multiple variable declarations

FIRST_NAME="Alice"
LAST_NAME="Smith"
AGE=25
FAVORITE_COLOR="blue"

echo "${FIRST_NAME} ${LAST_NAME} is learning Bash scripting."
echo "She is ${AGE} years old."
echo "Her favorite color is ${FAVORITE_COLOR}."
```

### Running the Script
1. **Create the script file:**
    ```bash
    touch multiple_variables.sh
    ```

2. **Give execute permission to the file:**
    ```bash
    chmod +x multiple_variables.sh
    ```

3. **Edit the script file:**
    ```bash
    vim multiple_variables.sh
    ```

4. **Insert the script and save the file:**
    ```bash
    #!/bin/bash
    # Description: Example of multiple variable declarations

    FIRST_NAME="Alice"
    LAST_NAME="Smith"
    AGE=25
    FAVORITE_COLOR="blue"

    echo "${FIRST_NAME} ${LAST_NAME} is learning Bash scripting."
    echo "She is ${AGE} years old."
    echo "Her favorite color is ${FAVORITE_COLOR}."
    ```
    - In `vim`, press `i` to insert the commands.
    - Save and quit `vim` by pressing `Esc` and typing `:wq`.

5. **Run the script:**
    ```bash
    ./multiple_variables.sh
    ```

## Summary
Variables in scripting allow for dynamic data manipulation and automation. By understanding how to declare and use variables, you can write more efficient and powerful scripts.
