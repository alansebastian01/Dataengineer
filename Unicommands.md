Absolutely. Here are some commonly used Unix/Linux commands with examples.

### File and Directory Commands

```bash
pwd
```

Displays the current working directory.

```bash
ls
```

Lists files and directories.

```bash
ls -l
```

Shows a detailed file listing.

```bash
ls -la
```

Shows all files, including hidden ones.

```bash
cd Documents
```

Changes to the `Documents` directory.

```bash
cd ..
```

Moves up one directory.

```bash
mkdir project
```

Creates a new directory named `project`.

```bash
rmdir project
```

Removes an empty directory.

---

### File Operations

```bash
touch notes.txt
```

Creates an empty file.

```bash
cp notes.txt backup.txt
```

Copies a file.

```bash
mv backup.txt archive.txt
```

Renames or moves a file.

```bash
rm archive.txt
```

Deletes a file.

```bash
rm -r old_folder
```

Deletes a directory and its contents.

---

### Viewing File Contents

```bash
cat notes.txt
```

Displays the entire file.

```bash
less notes.txt
```

Views a file one page at a time.

```bash
head notes.txt
```

Shows the first 10 lines.

```bash
tail notes.txt
```

Shows the last 10 lines.

```bash
tail -f logfile.log
```

Continuously monitors a log file.

---

### Searching

```bash
find . -name "*.txt"
```

Finds all `.txt` files in the current directory.

```bash
grep "error" logfile.log
```

Searches for the word "error" in a file.

```bash
grep -r "main" .
```

Recursively searches for "main" in all files.

---

### Permissions

```bash
chmod 755 script.sh
```

Changes file permissions.

```bash
chmod +x script.sh
```

Makes a script executable.

```bash
chown user:user file.txt
```

Changes the owner of a file.

---

### Process Management

```bash
ps
```

Lists running processes.

```bash
top
```

Displays real-time system activity.

```bash
kill 1234
```

Terminates the process with PID 1234.

```bash
kill -9 1234
```

Forcefully terminates the process.

---

### Disk Usage

```bash
df -h
```

Shows disk space usage.

```bash
du -sh Documents
```

Shows the size of the `Documents` directory.

---

### Networking

```bash
ping google.com
```

Checks network connectivity.

```bash
curl https://example.com
```

Fetches a web page.

```bash
wget https://example.com/file.zip
```

Downloads a file.

---

### Archives

```bash
tar -cvf archive.tar folder/
```

Creates a tar archive.

```bash
tar -xvf archive.tar
```

Extracts a tar archive.

```bash
zip files.zip file1.txt file2.txt
```

Creates a ZIP archive.

```bash
unzip files.zip
```

Extracts a ZIP archive.

---

### Useful Shortcuts

```bash
history
```

Displays previously executed commands.

```bash
clear
```

Clears the terminal screen.

```bash
man ls
```

Displays the manual page for the `ls` command.

```bash
echo "Hello, World!"
```

Prints text to the terminal.

---

### Example Workflow

```bash
mkdir unix_demo
cd unix_demo
touch file1.txt
echo "Hello Unix" > file1.txt
cat file1.txt
cp file1.txt backup.txt
ls -l
grep "Unix" file1.txt
rm backup.txt
pwd
```

This workflow creates a directory, creates a file, writes text into it, displays its contents, copies it, lists files, searches within the file, removes the copy, and prints the current directory.

If you're learning Unix for a class, I can also provide a **Top 50 Unix commands cheat sheet** or **practice exercises with solutions**.
