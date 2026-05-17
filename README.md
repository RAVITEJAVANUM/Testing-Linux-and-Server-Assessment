# Testing, Linux and Server Assessment

This project demonstrates Linux file management, permissions, ownership handling, and shell scripting using a Linux environment.

---

# Question 1: File Management and Permissions

## Objective

Create a complete project directory structure from scratch, apply correct permissions, and set ownership using Linux commands.

---

## Project Structure

```text
/home/ec2-user/webapp/
├── scripts/
├── logs/
│   └── app.log
└── config/
    └── app.conf
```

---

### Step 1: Create Directories

#### Command

```bash
sudo mkdir -p /home/ec2-user/webapp/{scripts,logs,config}
```

#### Screenshot

![Create Directories](Screenshots/q1-create-directories.png)

---

### Step 2: Create Configuration File

#### Command

```bash
cat > /home/ec2-user/webapp/config/app.conf
```

#### Content Added

```text
APP_NAME=WebApp
PORT=8080
```

Save the file using:

```text
Ctrl + D
```

#### Screenshot

![Create Config](Screenshots/q1-create-config.png)

---

### Step 3: Create Empty Log File

#### Command

```bash
touch /home/ec2-user/webapp/logs/app.log

ls -l /home/ec2-user/webapp/logs/app.log
```

#### Screenshot

![Create Log File](Screenshots/q1-create-log-file.png)

The `0` confirms the file is empty (0 bytes).

### Step 4: Set Permissions

#### Commands

```bash
chmod 755 /home/ec2-user/webapp/scripts
chmod 644 /home/ec2-user/webapp/config/app.conf
```

#### Permission Explanation

##### 755

| User | Permission |
|---|---|
| Owner | Read, Write, Execute |
| Group | Read, Execute |
| Others | Read, Execute |

##### 644

| User | Permission |
|---|---|
| Owner | Read, Write |
| Group | Read |
| Others | Read |

#### Screenshot

![Set Permissions](Screenshots/q1-set-permissions.png)

---

### Step 5: Change Ownership

#### Command

```bash
sudo chown -R root:root /home/ec2-user/webapp/
```

#### Screenshot

![Change Ownership](Screenshots/q1-change-ownership.png)

---

### Step 6: Verify Final Structure

#### Command

```bash
ls -lR /home/ec2-user/webapp/
```

#### Screenshot

![Output Structure](Screenshots/q1-output-structure.png)

---

## Final Output

```text
/home/ec2-user/webapp:
total 12
drwxr-xr-x 2 root root 22 May 17 config
drwxr-xr-x 2 root root 21 May 17 logs
drwxr-xr-x 2 root root  6 May 17 scripts

/home/ec2-user/webapp/config:
total 4
-rw-r--r-- 1 root root 30 May 17 app.conf

/home/ec2-user/webapp/logs:
total 0
-rw-r--r-- 1 root root 0 May 17 app.log

/home/ec2-user/webapp/scripts:
total 0
```

---

# Question 2: Creating an Interactive Log Script

## Objective

Using the `webapp/` structure from Question 1, create a bash script that:

- Takes user input
- Reads configuration data from `app.conf`
- Writes timestamped log entries
- Displays the log file contents

---

## Script Location

```text
/home/ec2-user/webapp/scripts/log_user.sh
```

---

### Step 1: Navigate to Scripts Directory

#### Command

```bash
cd /home/ec2-user/webapp/scripts/
```

#### Screenshot

![Navigate Directory](Screenshots/q2-navigate-directory.png)

---

### Step 2: Create Script File Using Vim

#### Command

```bash
vim log_user.sh
```

Press:

```text
i
```

to enter insert mode.

#### Screenshot

![Create Script](Screenshots/q2-create-script.png)

---

### Step 3: Add Script Content

#### Script Content

```bash
#!/bin/bash

read -p "Enter your name: " username

cat /home/ec2-user/webapp/config/app.conf

echo "Login: $username Date: $(date)" >> /home/ec2-user/webapp/logs/app.log

cat /home/ec2-user/webapp/logs/app.log
```

Save and exit using:

```text
Esc -> :wq
```

#### Screenshot

![Script Content](Screenshots/q2-script-content.png)

---

### Step 4: Give Execute Permission

#### Command

```bash
chmod +x log_user.sh
```

#### Screenshot

![Execute Permission](Screenshots/q2-execute-permission.png)

---

### Step 5: Run the Script Multiple Times

#### Command

```bash
./log_user.sh
```

The script was executed 3 times using different usernames.

#### Screenshots

![Run Script 1](Screenshots/q2-run-script-1.png)

![Run Script 2](Screenshots/q2-run-script-2.png)

![Run Script 3](Screenshots/q2-run-script-3.png)

---

### Step 6: Verify Log File Entries

#### Command

```bash
cat /home/ec2-user/webapp/logs/app.log
```

#### Screenshot

![Final Log Output](Screenshots/q2-final-log-output.png)

---

## Final Output

```text
Login: Chirag Date: Sat May 17 20:10:15 UTC 2026
Login: Priya Date: Sat May 17 20:11:03 UTC 2026
Login: Ravi Date: Sat May 17 20:12:44 UTC 2026
```
