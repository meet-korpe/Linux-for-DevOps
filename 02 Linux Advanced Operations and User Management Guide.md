### 1. Advanced File and Directory Operations

Building on the basics, these commands handle moving, renaming, and removing directories.

- **Moving and Renaming (mv):**
  - **Rename/Move a file:** `mv file1 file2` (renames file1 to file2 or moves it if the destination is a different path)
  - **Cut and Paste:** Effectively, `mv` acts as a "cut and paste" command
- **Directory Management:**
  - **Create a directory:** `mkdir dir_name`
  - **Remove an empty directory:** `rmdir dir_name`
  - **Remove parent and child directories:** `rmdir -p dir2/dir3` (removes both if they become empty)
  - **Remove files:** `rm filename`. Use `rm -rf` to forcefully and recursively remove directories and their contents
- **Navigation:**
  - **Change directory:** `cd [path]`
  - **Go up one level:** `cd ..`
  - **Check current path:** `pwd` (print working directory)

### 2. Enhanced Copying (cp) Commands

The `cp` command has several powerful flags for specific tasks:

- **Recursive Copy (`-r`):** `cp -r source_dir destination_dir` (copies a directory and all its contents)
- **Verbose Mode (`-v`):** `cp -v source destination` (shows a step-by-step list of what is being copied)
- **Interactive Mode (`-i`):** `cp -i file1 file2` (prompts for confirmation before overwriting an existing file)
- **Forceful Copy (`-f`):** `cp -f source destination` (forces the copy even if there are permission issues or existing files)
- **Update Copy (`-u`):** `cp -u source destination` (only copies if the source file is newer than the destination or doesn't exist)
- **Wildcard (`*`):** `cp /project/* /backup/` (copies **all** files from the project folder to the backup folder)

### 3. Hidden Files

In Linux, hidden files are used for configuration and are not shown by standard commands.

- **Identification:** Any file or directory starting with a dot (e.g., `.java` or `.dir1`) is **hidden**
- **Viewing:** Use `ls -a` (all) to see both regular and hidden files in a directory

### 4. Linux File Types and Permissions

A detailed look at how Linux identifies files and displays their metadata in a long listing (`ls -l`):

- **The 7 Types of Linux Files:**
  - `-` : Regular file
  - `d` : Directory
  - `l` : Symbolic link (shortcut)
  - `b` : Block file (hardware devices like hard drives)
  - `c` : Character file (devices like terminals or mice)
  - `s` : Socket file
  - `p` : Pipe files
- **Understanding `ls -l` Output:**
  - **Permissions:** (e.g., `rw-r--r--`)
  - **Linkcount:** Number of links to the file
  - **Owner & Group:** The user and group that own the file
  - **Size:** File size in bytes
  - **Timestamp:** Last modification date and time
  - **Filename:** The name of the file
  - **Storage Units:** Linux uses a binary scale: 1024 bytes = 1 KB; 1024 KB = 1 MB; 1024 MB = 1 GB, and so on

### 5. User Management

Managing who can access the system and their credentials.

- **Basic Commands:**
  - **Add a user:** `useradd username`
  - **Set/Change password:** `passwd username`
  - **Delete a user:** `userdel username`
  - **Check user info:** `id username`
- **Critical System Files:**
  - `/etc/passwd`: Stores **all user information** (view the end with `tail -5 /etc/passwd`)
  - `/etc/shadow`: Stores **all encrypted user passwords**
  - `/etc/group`: Stores **group information**


