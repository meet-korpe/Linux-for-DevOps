# Linux Shells and Scripting Essentials

## 1. Understanding the Shell

The shell is a program that acts as an **interpreter** between the user and the system. It interprets your commands and passes them to the kernel.

- **System Hierarchy:** The flow of communication is: **User → Shell → Kernel → OS**.
- **Analogy:**
  - **Hotel:** Operating System.
  - **Chef:** Kernel.
  - **Waiter:** Shell (takes your "order" or command and brings it to the "chef" or kernel).
  - **You (User):** The one placing the order.
- **Terminal vs. Shell:** The **terminal** is like a car, while the **shell** is the driver that actually operates the machine.

## 2. Types of Shells

There are several types of shells available in Linux, which can be viewed using the command `cat /etc/shells`.

1. **bash (Bourne Again Shell):** The default shell for most Linux distributions.
2. **sh (Bourne Shell):** The original UNIX shell.
3. **ksh (Korn Shell)**.
4. **csh (C Shell)**.
5. **tcsh**.
6. **zsh**.
7. **fish:** A "friendly interactive shell".

- **Check Current Shell:** Use the command `echo $SHELL`.

## 3. Shell Scripting Basics

**Shell Scripting** is the process of writing a series of Linux commands in a single file to **automate repetitive tasks** by executing them in sequence.

### A. Workflow to Create and Run a Script

1. **Create the file:** `touch script_name.sh`
2. **Write the script:** Use an editor like `vim script_name.sh`
3. **Grant execution permissions:** `chmod +x script_name.sh`
4. **Run the script:** `./script_name.sh`

### B. Script Components

- **Shebang (`#!`):** The first line of a script that tells the system which interpreter to use (e.g., `#!/bin/bash`).
- **Variables:** Used to store values.
  - **Definition:** `chocolate="eclair"`
  - **Usage:** `echo $chocolate` (Outputs "eclair").
- **User Input:** Use the read command to capture input from the user (e.g., `read name`).

## 4. Comparison Operators and Logic

When writing scripts with conditional logic, specific operators are used for comparisons.

| Operator | Description |
|---|---|
| `-eq` | Equal to |
| `-ne` | Not equal to |
| `-gt` | Greater than |
| `-lt` | Less than |
| `-ge` | Greater than or equal to |
| `-le` | Less than or equal to |

### Programming Structures

- **Conditionals:** if-else, if-elif-else, and case statements.
- **Loops:** for loop, while loop, and until loop.
- **Advanced Features:** Functions and arrays.