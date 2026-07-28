# Bash Scripts and Command Logic

## 1. Number Parity (Even or Odd) Script

```bash
#!/bin/bash
echo "ENTER A NUMBER"
read num

if [ $((num % 2)) -eq 0 ]
then
  echo "$num is EVEN"
else
  echo "$num is ODD"
fi
```

**Explanation:**

- **#!/bin/bash**: The shebang line that tells the system to use the bash interpreter to run this script.
- **echo "ENTER A NUMBER"**: Displays a prompt to the user.
- **read num**: Takes the user's input and stores it in the variable num.
- **if [ $((num % 2)) -eq 0 ]**: This uses the modulo operator (%) to find the remainder of the number when divided by 2. If the remainder is equal (-eq) to 0, the number is even.
- **then/else/fi**: Standard conditional structure to output whether the number is **EVEN** or **ODD**.

## 2. Voting Eligibility Script

```bash
#!/bin/bash
echo "ENTER YOUR AGE"
read age

if [ $age -ge 18 ]
then
  echo "ELIGIBLE TO VOTE"
else
  echo "NOT ELIGIBLE TO VOTE"
fi
```

**Explanation:**

- **read age**: Captures the user's age as input.
- **if [ $age -ge 18 ]**: Uses the **-ge** operator (greater than or equal to) to check if the age is 18 or older.
- **then/else**: Displays the appropriate eligibility message based on the numeric comparison.

## 3. File Existence Checker Script

```bash
#!/bin/bash
echo "ENTER FILENAME"
read file

if [ -f "$file" ]
then
  echo "file is exist"
else
  echo "file not found"
fi
```

**Explanation:**

- **read file**: Stores the filename or path entered by the user.
- **if [ -f "$file" ]**: The **-f** flag is a file test operator that checks if the specified path exists and is a regular file (not a directory).
- **then/else**: Informs the user whether the file was successfully located in the system.

## 4. Home Directory Backup Script

```bash
#!/bin/bash
tar -czvf ramubackup.tar.gz /home/ramu
echo "Backup completed successfully"
```

**Explanation:**

- **tar -czvf ...**: This command automates the archival process.
- **-c**: Create a new archive.
- **-z**: Compress the archive using gzip.
- **-v**: Verbose mode, which lists all files being added to the archive.
- **-f**: Specifies the name of the destination file (ramubackup.tar.gz).
- **echo "Backup completed..."**: Provides a status message once the backup operation is finished.

## 5. Dynamic Service Management Script

```bash
#!/bin/bash
echo "enter service name:"
read service

service "$service" status
```

**Explanation:**

- **read service**: Allows the user to specify which system service (like httpd, crond, or iptables) they want to check.
- **service "$service" status**: Executes the system service command using the name provided by the user to display its current operational state.

