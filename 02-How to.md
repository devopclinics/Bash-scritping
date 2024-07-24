# How to Write a Script

## Steps to Create a Simple Bash Script

### 1. Determine the Shell
Check the current shell you are using:
```bash
echo $SHELL
```

### 2. Create the Script File
Use the `touch` command to create a new script file named `hello.sh`:
```bash
touch hello.sh
```

### 3. Give Execute Permission to the File
Use the `chmod` command to make the script executable:
```bash
chmod +x hello.sh
```

### 4. Edit the Script File
Open the script file using a text editor like `vim`:
```bash
vim hello.sh
```

### 5. Insert Commands
In `vim`, press `i` to enter insert mode and add the following command to display "Hello World":
```bash
echo "Hello World"
```
Then, save and quit `vim` by pressing `Esc` and typing `:wq`.

### 6. Run the Script
Execute the script using the following command:
```bash
./hello.sh
```

### Example: Hello World Script
Here is a step-by-step example to create a "Hello World" script:

1. **Create the script file:**
    ```bash
    touch hello.sh
    ```

2. **Give execute permission to the file:**
    ```bash
    chmod +x hello.sh
    ```

3. **Edit the script file:**
    ```bash
    vim hello.sh
    ```

4. **Insert the command and save the file:**
    ```bash
    echo "Hello World"
    ```
    - In `vim`, press `i` to insert the command.
    - Save and quit `vim` by pressing `Esc` and typing `:wq`.

5. **Run the script:**
    ```bash
    ./hello.sh
    ```
