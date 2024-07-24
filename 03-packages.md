# Script to Install Packages in Linux

## Creating a Bash Script to Automate Package Installation

### Step-by-Step Approach

### 1. Create the Script File
Use the `touch` command to create a new script file named `packages.sh`:
```bash
touch packages.sh
```

### 2. Give Execute Permission to the File
Use the `chmod` command to make the script executable:
```bash
chmod +x packages.sh
```

### 3. Edit the Script File
Open the script file using a text editor like `vim`:
```bash
vim packages.sh
```

### 4. Insert the Commands
In `vim`, press `i` to enter insert mode and add the following script to automate the installation of packages:
```bash
#!/bin/bash

# Description: It automates the installation of packages
# Author: Mur Ami
# Date: 07262021

yum install finger -y
yum install curl -y
yum install zip -y
yum install vim -y
```
Then, save and quit `vim` by pressing `Esc` and typing `:wq`.

### 5. Run the Script
Execute the script using the following command:
```bash
./packages.sh
```

### Example: packages.sh Script
Here is the complete example of the `packages.sh` script:

```bash
#!/bin/bash

# Description: It automates the installation of packages
# Author: Mur Ami
# Date: 07262021

yum install finger -y
yum install curl -y
yum install zip -y
yum install vim -y
```

### Summary of Steps

1. **Create the script file:**
    ```bash
    touch packages.sh
    ```

2. **Give execute permission to the file:**
    ```bash
    chmod +x packages.sh
    ```

3. **Edit the script file:**
    ```bash
    vim packages.sh
    ```

4. **Insert the commands and save the file:**
    ```bash
    #!/bin/bash

    # Description: It automates the installation of packages
    # Author: Mur Ami
    # Date: 07262021

    yum install finger -y
    yum install curl -y
    yum install zip -y
    yum install vim -y
    ```
    - In `vim`, press `i` to insert the commands.
    - Save and quit `vim` by pressing `Esc` and typing `:wq`.

5. **Run the script:**
    ```bash
    ./packages.sh
    ```