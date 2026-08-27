# Bash Scripting — Basics and Quick Reference

## 1. What is Bash?

**Bash** stands for **Bourne Again Shell**.

Bash is both:

- A **shell** — a program that lets you interact with the operating system by entering commands.
- A **scripting language** — a language used to put commands, variables, conditions, loops, and functions into a file and automate tasks.

For example, interactively:

```bash
ls
pwd
grep "ERROR" application.log
```

The same commands can be placed into a Bash script and executed automatically.

### Bash scripting

**Bash scripting** means writing a sequence of commands and Bash logic in a file, usually with a `.sh` extension, so that the tasks can be executed repeatedly or automatically.

Typical DevOps uses include:

- Checking services
- Monitoring disk usage
- Processing logs
- Creating backups
- Automating deployments
- Running system administration tasks

---

# 2. Different Shells

A **shell** is a command interpreter. Bash is one type of shell, but Linux/Unix systems can have several shells.

| Shell | Description |
|---|---|
| `sh` | Traditional/POSIX shell interface |
| `bash` | Bourne Again Shell; very common and feature-rich |
| `dash` | Small, fast POSIX-compliant shell |
| `zsh` | Feature-rich shell, popular for interactive use |
| `fish` | User-friendly shell with syntax different from Bash |

Check available shells:

```bash
cat /etc/shells
```

Check your current shell:

```bash
echo "$SHELL"
```

On Ubuntu, `/bin/sh` is commonly linked to `dash`.

```bash
ls -l /bin/sh
```

You may see:

```text
/bin/sh -> dash
```

### Bash vs sh/dash

Bash provides features beyond basic POSIX shell syntax.

For example, Bash supports arrays:

```bash
names=("Alice" "Bob" "Charlie")
echo "${names[0]}"
```

If a script specifically requires Bash features, use a Bash shebang:

```bash
#!/bin/bash
```

If a script is intended to be POSIX-compatible, it can use:

```bash
#!/bin/sh
```

---

# 3. Shebang

A **shebang** is the first line of an executable script that specifies which interpreter should execute the file.

Example:

```bash
#!/bin/bash
```

It tells the operating system:

> Execute this script using Bash.

Other examples:

```bash
#!/bin/sh
#!/bin/dash
#!/usr/bin/env bash
```

### Why use a shebang?

Without a shebang, directly executing a script does not clearly specify which interpreter should interpret the script.

For example:

```bash
#!/bin/bash

name="Ujwala"
echo "Hello $name"
```

When executed as:

```bash
./hello.sh
```

the system uses Bash because of:

```bash
#!/bin/bash
```

### `/bin/bash` vs `/usr/bin/env bash`

```bash
#!/bin/bash
```

uses Bash at a specific path.

```bash
#!/usr/bin/env bash
```

asks `env` to find `bash` using the system's `PATH`.

For learning Bash, this is straightforward:

```bash
#!/bin/bash
```

---

# 4. Executing a Script/File

Suppose we have:

```text
script.sh
```

There are two common ways to execute it.

## Method 1 — Execute the file directly

First make it executable:

```bash
chmod +x script.sh
```

Then:

```bash
./script.sh
```

Here:

- `./` means the file is in the **current directory**.
- The executable permission is required.
- The shebang determines which interpreter should run it.

Flow:

```text
./script.sh
    ↓
read shebang
    ↓
#!/bin/bash
    ↓
execute using Bash
```

## Method 2 — Explicitly run it with Bash

```bash
bash script.sh
```

Here you explicitly tell Bash to interpret the file.

The executable permission is not required for this method.

### Important distinction

```bash
./script.sh
```

Uses the script's shebang.

```bash
bash script.sh
```

Explicitly uses Bash.

For example, even if a script has:

```bash
#!/bin/sh
```

you can technically run:

```bash
bash script.sh
```

and Bash will interpret it.

---

# 5. Comments

Comments are ignored by Bash.

A comment begins with:

```bash
#
```

Example:

```bash
#!/bin/bash

# This is a comment
echo "Hello"
```

Comments are useful for explaining what a section of a script does.

Example:

```bash
# Check whether the service is running
systemctl is-active nginx
```

The shebang also starts with `#`, but it has special meaning when the file is executed directly.

---

# 6. Variables

Variables store values.

## Creating variables

Basic syntax:

```bash
variable=value
```

There must be **no spaces around `=`**.

Correct:

```bash
name="Ujwala"
age=25
```

Incorrect:

```bash
name = "Ujwala"
```

Bash would interpret this differently and produce an error.

## Accessing a variable

Use `$`:

```bash
name="Ujwala"

echo "$name"
```

Output:

```text
Ujwala
```

You can also use braces:

```bash
echo "${name}"
```

Braces are especially useful when adding text directly after a variable:

```bash
name="Ujwala"

echo "${name}_backup"
```

Output:

```text
Ujwala_backup
```

---

## 6.1 Numeric variables

Bash does not require a special declaration for normal integer variables.

```bash
age=25
count=10
```

You can perform arithmetic using:

```bash
sum=$((age + count))
```

Example:

```bash
a=10
b=5

sum=$((a + b))
echo "$sum"
```

Output:

```text
15
```

Bash variables are generally treated as strings unless used in an arithmetic context.

---

## 6.2 String variables

```bash
name="Ujwala"
message="Hello World"
```

Strings can contain spaces when quoted:

```bash
message="Hello World"
```

---

## 6.3 Command output stored in a variable

This is called **command substitution**:

```bash
hostname=$(hostname)
```

The command:

```bash
hostname
```

is executed and its output is stored in the variable.

Example:

```bash
current_date=$(date)

echo "$current_date"
```

---

## 6.4 Environment variables

Linux provides many environment variables:

```bash
echo "$HOME"
echo "$USER"
echo "$PATH"
echo "$SHELL"
```

View environment variables:

```bash
env
```

or:

```bash
printenv
```

A variable can be exported so that child processes can access it:

```bash
export APP_ENV="production"
```

---

# 7. Single Quotes vs Double Quotes

This distinction is very important in Bash.

## Double quotes `"..."`

Variables and command substitutions are expanded inside double quotes.

```bash
name="Ujwala"

echo "Hello $name"
```

Output:

```text
Hello Ujwala
```

Command substitution also works:

```bash
echo "Today is $(date)"
```

## Single quotes `'...'`

Everything inside single quotes is treated literally.

```bash
name="Ujwala"

echo 'Hello $name'
```

Output:

```text
Hello $name
```

The variable is **not expanded**.

### Quick comparison

| Syntax | Variable expansion | Command substitution |
|---|---|---|
| `"..."` | Yes | Yes |
| `'...'` | No | No |

### Rule of thumb

Use double quotes when you want variables to expand:

```bash
echo "$name"
```

Use single quotes when you want the content treated literally:

```bash
echo '$name'
```

---

# 8. Command Substitution

Command substitution means:

> Execute a command and use its output as a value.

Preferred syntax:

```bash
$(command)
```

Example:

```bash
hostname=$(hostname)
```

Another example:

```bash
files=$(ls)
echo "$files"
```

You can also use command substitution directly:

```bash
echo "Current date: $(date)"
```

### Older syntax

You may encounter:

```bash
`hostname`
```

This is older command-substitution syntax.

Prefer:

```bash
$(hostname)
```

because it is easier to read and nest.

---

# 9. Reading User Input

Use `read`.

Example:

```bash
echo "Enter your name:"
read name

echo "Hello $name"
```

A shorter form:

```bash
read -p "Enter your name: " name

echo "Hello $name"
```

The entered value is stored in `name`.

---

# 10. Command-Line Arguments

Arguments are values supplied when running the script.

Suppose:

```bash
./backup.sh test.txt backup/
```

Bash provides special positional parameters:

| Variable | Meaning |
|---|---|
| `$0` | Script name |
| `$1` | First argument |
| `$2` | Second argument |
| `$3` | Third argument |
| `$#` | Number of arguments |
| `$@` | All arguments |
| `$?` | Exit status of previous command |
| `$$` | Process ID of current shell/script |

Example:

```bash
#!/bin/bash

echo "Script: $0"
echo "First argument: $1"
echo "Second argument: $2"
echo "Number of arguments: $#"
```

Run:

```bash
./script.sh file.txt backup
```

Result conceptually:

```text
$0 → ./script.sh
$1 → file.txt
$2 → backup
$# → 2
```

---

# 11. All Arguments — `$@`

`$@` represents all command-line arguments.

Example:

```bash
#!/bin/bash

for item in "$@"; do
    echo "$item"
done
```

Run:

```bash
./script.sh file1.txt file2.txt file3.txt
```

Output:

```text
file1.txt
file2.txt
file3.txt
```

This is useful when a script needs to process an unknown number of arguments.

---

# 12. Exit Codes

Linux commands return an **exit status**.

Convention:

```text
0       → success
non-zero → failure/error
```

Check the exit status of the previous command:

```bash
echo $?
```

Example:

```bash
ls /tmp
echo $?
```

If `ls` succeeds:

```text
0
```

If a command fails:

```text
non-zero
```

You can explicitly set an exit code:

```bash
exit 0
```

or:

```bash
exit 1
```

Example:

```bash
if [ ! -f "$file" ]; then
    echo "File does not exist"
    exit 1
fi
```

Exit codes are especially important in DevOps because CI/CD systems, monitoring tools, and other scripts can use them to determine whether an operation succeeded.

---

# 13. Numeric Comparison Operators

Bash uses special operators for numeric comparisons.

| Operator | Meaning |
|---|---|
| `-eq` | Equal |
| `-ne` | Not equal |
| `-gt` | Greater than |
| `-ge` | Greater than or equal |
| `-lt` | Less than |
| `-le` | Less than or equal |

Examples:

```bash
if [ "$age" -ge 18 ]; then
    echo "Adult"
fi
```

```bash
if [ "$usage" -gt 80 ]; then
    echo "High usage"
fi
```

Important:

```bash
[ "$a" -gt "$b" ]
```

is different from:

```bash
[ "$a" > "$b" ]
```

For numeric comparisons inside `[ ]`, use `-gt`, `-lt`, etc.

---

# 14. String Comparison Operators

Common string operators:

| Operator | Meaning |
|---|---|
| `=` | Strings are equal |
| `!=` | Strings are not equal |
| `-z` | String is empty |
| `-n` | String is not empty |

Example:

```bash
name="admin"

if [ "$name" = "admin" ]; then
    echo "Administrator"
fi
```

Check whether a variable is empty:

```bash
if [ -z "$name" ]; then
    echo "Name not provided"
fi
```

Check whether it is not empty:

```bash
if [ -n "$name" ]; then
    echo "Name provided"
fi
```

---

# 15. Logical Operators

Logical operators allow multiple conditions to be combined.

## AND — `&&`

Both conditions must succeed.

```bash
if [ "$age" -ge 18 ] && [ "$country" = "India" ]; then
    echo "Condition met"
fi
```

Conceptually:

```text
Condition 1 AND Condition 2
        ↓
     both true
        ↓
      execute
```

## OR — `||`

At least one condition must succeed.

```bash
if [ "$x" -eq 1 ] || [ "$x" -eq 2 ]; then
    echo "Valid"
fi
```

## NOT — `!`

Reverses a condition.

```bash
if [ ! -f "$file" ]; then
    echo "File does not exist"
fi
```

Here:

```text
-f → file exists
!-f → file does NOT exist
```

---

# 16. `if`

Basic structure:

```bash
if condition; then
    commands
fi
```

Example:

```bash
if [ "$age" -ge 18 ]; then
    echo "Adult"
fi
```

Important parts:

```text
if       → start condition
then     → commands to execute if true
fi       → end if
```

---

# 17. `if ... else`

Use `else` when there are two possible paths.

```bash
if [ "$age" -ge 18 ]; then
    echo "Adult"
else
    echo "Minor"
fi
```

Flow:

```text
       condition
        /     \
     true     false
      ↓         ↓
    then      else
```

---

# 18. `if ... elif ... else`

Use this when there are multiple conditions.

```bash
if [ "$usage" -ge 90 ]; then
    echo "Critical"
elif [ "$usage" -ge 80 ]; then
    echo "Warning"
else
    echo "Normal"
fi
```

Flow:

```text
usage >= 90?
    ↓
   yes → Critical

   no
    ↓
usage >= 80?
    ↓
   yes → Warning

   no
    ↓
 Normal
```

---

# 19. `[ ]` Conditions

You will frequently see:

```bash
[ condition ]
```

Example:

```bash
if [ "$age" -ge 18 ]; then
    echo "Adult"
fi
```

The spaces are important.

Correct:

```bash
[ "$age" -ge 18 ]
```

Incorrect:

```bash
["$age" -ge 18]
```

`[` is actually a command (the `test` command in another form), which is why proper spacing is required.

---

# 20. File Tests

Bash provides operators for checking files and directories.

| Test | Meaning |
|---|---|
| `-f file` | Regular file exists |
| `-d dir` | Directory exists |
| `-e path` | Path exists |
| `-r file` | File is readable |
| `-w file` | File is writable |
| `-x file` | File is executable |
| `-s file` | File exists and is not empty |

Examples:

```bash
if [ -f "$file" ]; then
    echo "File exists"
fi
```

Directory:

```bash
if [ -d "$directory" ]; then
    echo "Directory exists"
fi
```

Negation:

```bash
if [ ! -f "$file" ]; then
    echo "File does not exist"
fi
```

---

# 21. `case`

`case` is useful when a variable can have several known values.

Example:

```bash
case "$environment" in
    dev)
        echo "Development"
        ;;
    test)
        echo "Testing"
        ;;
    prod)
        echo "Production"
        ;;
    *)
        echo "Unknown environment"
        ;;
esac
```

If:

```bash
environment="prod"
```

the output is:

```text
Production
```

### Structure

```bash
case "$variable" in
    value1)
        commands
        ;;
    value2)
        commands
        ;;
    *)
        default commands
        ;;
esac
```

`*` acts as the default case.

`;;` ends each case branch.

---

# 22. `for` Loop

A `for` loop repeats commands for each item.

Example:

```bash
for name in Alice Bob Charlie; do
    echo "Hello $name"
done
```

Output:

```text
Hello Alice
Hello Bob
Hello Charlie
```

### Loop through files

Very common in Bash:

```bash
for file in *.log; do
    echo "Processing $file"
done
```

This processes every `.log` file in the current directory.

### Loop through all arguments

```bash
for file in "$@"; do
    echo "Processing $file"
done
```

---

# 23. `while` Loop

A `while` loop continues while its condition is true.

Example:

```bash
count=1

while [ "$count" -le 5 ]; do
    echo "$count"
    count=$((count + 1))
done
```

Output:

```text
1
2
3
4
5
```

Flow:

```text
Check condition
      ↓
    true?
    /   \
  yes    no
   ↓      ↓
execute   stop
   ↓
repeat
```

Be careful to change the variable used in the condition, otherwise you can create an infinite loop.

---

# 24. Functions

Functions allow you to group reusable commands.

Basic syntax:

```bash
function_name() {
    commands
}
```

Example:

```bash
greet() {
    echo "Hello"
}

greet
```

Output:

```text
Hello
```

## Function arguments

Functions can have arguments just like scripts.

```bash
greet() {
    echo "Hello $1"
}

greet "Ujwala"
```

Output:

```text
Hello Ujwala
```

Here `$1` means the first argument **passed to the function**.

Example with a service:

```bash
check_service() {
    systemctl is-active --quiet "$1"
}

check_service cron
```

Functions are useful for avoiding repeated code.

---

# 25. `command1 && command2`

`&&` means:

> Execute command 2 only if command 1 succeeds.

Example:

```bash
mkdir backup && echo "Backup directory created"
```

If `mkdir` succeeds:

```text
Backup directory created
```

If `mkdir` fails, the `echo` command isn't executed.

Flow:

```text
command1
   ↓
success?
 /     \
yes     no
 ↓       ↓
cmd2    stop
```

This is commonly used for short success-dependent operations.

---

# 26. `command1 || command2`

`||` means:

> Execute command 2 only if command 1 fails.

Example:

```bash
systemctl is-active --quiet nginx || echo "Nginx is down"
```

If Nginx is running:

```text
nothing is printed
```

If Nginx is not running:

```text
Nginx is down
```

Flow:

```text
command1
   ↓
success?
 /     \
yes     no
 ↓       ↓
stop    cmd2
```

---

# 27. `&&` and `||` Together

You can combine them:

```bash
mkdir backup && echo "Created" || echo "Failed"
```

Conceptually:

```text
mkdir backup
     ↓
  success?
   /    \
 yes     no
 ↓       ↓
Created Failed
```

For complex scripts, however, an explicit `if` is often easier to read.

---

# 28. Putting Everything Together

A practical Bash script can combine all these concepts:

```bash
#!/bin/bash

threshold=80
service_name=$1

if [ -z "$service_name" ]; then
    echo "Usage: $0 <service>"
    exit 1
fi

check_service() {
    if systemctl is-active --quiet "$1"; then
        echo "$1 is running"
    else
        echo "$1 is not running"
        return 1
    fi
}

check_service "$service_name"

disk_usage=$(df / | awk 'NR==2 {print $5}' | tr -d '%')

if [ "$disk_usage" -ge "$threshold" ]; then
    echo "WARNING: Disk usage is $disk_usage%"
else
    echo "Disk usage is normal: $disk_usage%"
fi
```

This combines:

```text
Shebang
   ↓
Variables
   ↓
Command-line arguments
   ↓
Validation
   ↓
Functions
   ↓
Conditions
   ↓
systemctl
   ↓
Command substitution
   ↓
Pipes
   ↓
awk
   ↓
Numeric comparison
   ↓
Output / exit status
```

---

# 29. Bash Scripting Mental Model

The easiest way to remember Bash is:

```text
                    BASH SCRIPT
                         │
             ┌───────────┴───────────┐
             │                       │
           INPUT                    LOGIC
             │                       │
      ┌──────┼──────┐          ┌─────┼─────┐
      │      │      │          │     │     │
     read   $1     $@         if   case  loops
                                  │
                               functions
             │                       │
             └───────────┬───────────┘
                         ↓
                  Linux commands
                         │
              ┌──────────┼──────────┐
              ↓          ↓          ↓
             grep       awk       systemctl
              │          │          │
              └──────────┼──────────┘
                         ↓
                       OUTPUT
                         │
                     exit code
```

## The core idea

Bash scripting is primarily about taking the Linux commands you already know and combining them with:

- Variables
- Input
- Arguments
- Conditions
- Loops
- Functions
- Exit codes
- Pipes/redirection

to **automate system tasks**.

---

# 30. Quick Cheat Sheet

```bash
#!/bin/bash                  # Bash interpreter

# comment                    # Comment

name="Ujwala"                # Variable
age=25                       # Numeric value
echo "$name"                 # Use variable

result=$(date)               # Command substitution

read name                    # User input

$0                           # Script name
$1                           # First argument
$2                           # Second argument
$#                           # Number of arguments
$@                           # All arguments
$?                           # Previous exit status
$$                           # Current process ID

exit 0                       # Success
exit 1                       # Failure

[ "$a" -eq "$b" ]            # Numeric comparison
[ "$a" = "$b" ]              # String comparison
[ -f "$file" ]               # File exists
[ -d "$dir" ]                # Directory exists
[ -z "$value" ]              # Empty string

if ...; then ... fi          # Condition
if ...; then ... else ... fi # If/else

case "$x" in ... esac        # Multiple choices

for x in ...; do ... done    # For loop
while condition; do ... done # While loop

function_name() { ... }      # Function

cmd1 && cmd2                 # cmd2 if cmd1 succeeds
cmd1 || cmd2                 # cmd2 if cmd1 fails

command1 | command2          # Pipe
command > file               # Overwrite output
command >> file              # Append output
command 2> file              # Redirect errors

bash -x script.sh            # Debug/trace execution
```

---

# 31. What You Should Know for DevOps

### Must know

- Bash vs shell
- Shebang
- `./script.sh` vs `bash script.sh`
- Variables
- Quoting
- Command substitution
- User input
- Command-line arguments
- `$@`, `$#`, `$?`
- Exit codes
- `if/elif/else`
- `[ ]`
- File tests
- Numeric/string comparisons
- `for` and `while`
- Functions
- `case`
- `&&` and `||`
- Pipes and basic Linux commands

### Learn later

- `set -e`
- `set -u`
- `set -o pipefail`
- Arrays
- `getopts`
- `trap`
- Signals
- Advanced parameter expansion
- Process substitution

These advanced features are useful in production scripts, but they aren't necessary for your current Bash foundation.
