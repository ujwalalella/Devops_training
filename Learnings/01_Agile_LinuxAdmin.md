## 1. Agile Methodologies

### What is Agile?

**Agile** is a software development approach that delivers software in small increments, gets frequent feedback, and adapts to changing requirements.
Key for Continuous feedback & incremental delivery.

### Common Agile Methodologies / Frameworks

- **Scrum** — Work is organized into fixed-length iterations called Sprints with defined roles, events, and backlogs.
- **Kanban** — Work is visualized on a board and moved continuously through stages, with a focus on limiting work in progress.
- **Extreme Programming (XP)** — Focuses strongly on engineering practices such as pair programming, test-driven development, and continuous integration.
- **Scrumban** — Combines Scrum practices with Kanban's continuous flow and work-in-progress limits.

### Scrum

**Scrum** is an Agile framework where a team works on prioritized work in short, fixed iterations called **Sprints**.

### Sprint

A **Sprint** is a fixed period, commonly 1–4 weeks, during which the team develops and tests a selected set of work.

### Product Backlog

The **Product Backlog** is the prioritized list of all features, improvements, bugs, and other work that may be needed for the product.

### Sprint Backlog

The **Sprint Backlog** is the set of Product Backlog items selected for the current Sprint, along with the work needed to complete them.

### Daily Standup

A **Daily Standup** is a short daily meeting where team members discuss progress, today's work, and blockers.

### Sprint Review

A **Sprint Review** happens at the end of a Sprint to demonstrate the completed increment, collect feedback, and discuss what should come next.

---

# 2. Monolithic Architecture

### Definition

A **monolithic application** is an application where multiple business functionalities are implemented together and generally deployed as one unit.

### Mental Model

```text
             Monolithic Application
┌──────────────────────────────────────┐
│ Login │ Products │ Orders │ Payment │
└──────────────────────────────────────┘
                  ↓
            One deployment
```

### Cons / Disadvantages

- Scaling often requires scaling the whole application.
- A change in one part may require rebuilding and redeploying the entire application.
- Large codebases can become difficult to maintain.
- Components can become tightly coupled.
- A failure in one area can potentially affect the whole application.

---

# 3. Microservices Architecture

### Definition

**Microservices architecture** divides an application into small, independently deployable services, with each service generally responsible for a specific business capability.

### Mental Model

```text
              Application
                   │
       ┌───────────┼───────────┐
       ↓           ↓           ↓
   User Service Product     Payment
                  Service     Service
```

Each service can generally be developed, deployed, and scaled independently.

---

# 4. Linux Administration

Linux administration is the management of a Linux system's users, files, permissions, processes, software, services, storage, networking, and system resources.

---

## 4.1 Permissions

### Why?

Permissions control **who can read, modify, or execute files and directories**.

### Important Commands

- `ls -l` — Displays file ownership and read/write/execute permissions.
- `chmod` — Changes file or directory permissions.
- `chown` — Changes the owner of a file or directory.
- `chgrp` — Changes the group ownership.
- `umask` — Controls the default permissions assigned when new files/directories are created.
- `id` — Displays the current user's UID, GID, and group memberships.
- `whoami` — Displays the current username.
- `groups` — Displays the groups a user belongs to.

### Permission Values

```text
r = 4
w = 2
x = 1
```

Example:

```bash
chmod 755 script.sh
```

means owner = `rwx`, group = `r-x`, others = `r-x`.

---

## 4.2 Files & Directories

### Why?

File and directory administration is necessary to organize data, configuration, logs, applications, and system files.

### Important Commands

- `pwd` — Displays the current working directory.
- `ls` — Lists files and directories.
- `cd` — Changes the current directory.
- `mkdir` — Creates directories.
- `touch` — Creates an empty file or updates a file's timestamp.
- `cp` — Copies files or directories.
- `mv` — Moves or renames files or directories.
- `rm` — Removes files or directories.
- `cat` — Displays file contents.
- `less` — Views large files interactively.
- `head` — Displays the beginning of a file.
- `tail` — Displays the end of a file.
- `file` — Identifies the type of a file.
- `stat` — Displays detailed file metadata.
- `ln` — Creates hard or symbolic links.
- `df -h` — Displays filesystem disk usage.
- `du -sh` — Displays the size used by a file or directory.
- `lsblk` — Displays block devices and storage layout.
- `mount` — Mounts a filesystem.
- `umount` — Unmounts a filesystem.

---

## 4.3 Searching

### Why?

Searching helps administrators quickly locate files, directories, commands, and specific text in configuration files and logs.

### Important Commands

- `find` — Searches for files/directories based on conditions such as name, type, size, or time.
- `locate` — Searches a prebuilt database for file paths.
- `grep` — Searches for matching text inside files or command output.
- `which` — Shows the executable path used for a command.
- `whereis` — Locates a command's binary, source, and manual-page information.
- `type` — Shows how the shell interprets a command.

Examples:

```bash
find /var/log -name "*.log"
grep "ERROR" application.log
which python
```

---

## 4.4 Text Processing

### Why?

Text processing is essential for analyzing logs, configuration files, command output, and other text-based data.

### Important Commands

- `grep` — Searches for matching lines or patterns.
- `sed` — Performs stream-based text transformations and substitutions.
- `awk` — Processes structured text and extracts or manipulates fields.
- `cut` — Extracts selected columns or fields.
- `sort` — Sorts lines.
- `uniq` — Removes adjacent duplicate lines.
- `tr` — Translates, replaces, or deletes characters.
- `wc` — Counts lines, words, and bytes/characters.
- `tee` — Sends output to both the terminal and a file.
- `xargs` — Builds and executes commands using input from another command.
- `diff` — Compares two files line by line.

Example pipeline:

```bash
cat application.log | grep "ERROR" | sort | uniq
```

---

## 4.5 Processes

### Why?

Process management helps administrators monitor running applications, identify resource-consuming processes, and control processes.

### Important Commands

- `ps` — Displays information about running processes.
- `top` — Provides real-time process and resource monitoring.
- `htop` — Interactive process monitor when installed.
- `pgrep` — Finds process IDs based on process names or attributes.
- `pstree` — Displays processes in a parent-child tree.
- `kill` — Sends a signal to a process.
- `killall` — Sends a signal to processes matching a name.
- `jobs` — Displays jobs started from the current shell.
- `fg` — Brings a background job to the foreground.
- `bg` — Continues a stopped job in the background.
- `nohup` — Runs a command so it can continue after the terminal session ends.

### Important Signals

```text
SIGTERM (15) — Requests graceful termination.
SIGKILL (9)  — Forces termination and cannot be caught by the process.
```

---

## 4.6 Package Management

### Why?

Package management installs, updates, removes, and maintains software and its dependencies.

### Ubuntu/Debian — APT

- `apt update` — Refreshes the local package index.
- `apt upgrade` — Upgrades installed packages.
- `apt install` — Installs a package and required dependencies.
- `apt remove` — Removes a package while generally keeping configuration files.
- `apt purge` — Removes a package and its configuration files.
- `apt search` — Searches available packages.
- `apt show` — Displays package information.
- `apt list --installed` — Lists installed packages.
- `apt autoremove` — Removes automatically installed packages no longer required.

Example:

```bash
sudo apt update
sudo apt install nginx
```

---

## 4.7 Services / systemd

### Why?

Service management controls background applications such as SSH, web servers, databases, schedulers, and logging services.

### Important Concepts

- **systemd** — The system and service manager on many modern Linux distributions.
- **systemctl** — The command-line tool used to communicate with systemd.
- **journalctl** — Used to view logs collected by the systemd journal.

### Important Commands

- `systemctl status service` — Displays the current service status.
- `systemctl start service` — Starts a service now.
- `systemctl stop service` — Stops a service now.
- `systemctl restart service` — Restarts a service.
- `systemctl reload service` — Reloads configuration without a full restart when supported.
- `systemctl enable service` — Configures a service to start during boot.
- `systemctl disable service` — Prevents a service from starting automatically at boot.
- `systemctl enable --now service` — Enables and starts a service.
- `systemctl list-units --type=service` — Lists loaded service units.
- `journalctl -u service` — Displays logs for a specific service.
- `journalctl -u service -f` — Follows service logs in real time.

---

## 4.8 Archives

### Why?

Archives package multiple files/directories into a single file and are commonly used for backups, transfers, and application packaging.

### Important Commands

- `tar` — Creates and extracts archives.
- `gzip` — Compresses data using gzip.
- `gunzip` — Decompresses gzip files.
- `zip` — Creates ZIP archives.
- `unzip` — Extracts ZIP archives.

### Common `tar` Commands

```bash
tar -cvf backup.tar directory/
```

Creates a tar archive.

```bash
tar -xvf backup.tar
```

Extracts a tar archive.

```bash
tar -czvf backup.tar.gz directory/
```

Creates a gzip-compressed tar archive.

```bash
tar -xzvf backup.tar.gz
```

Extracts a gzip-compressed tar archive.

### Common `tar` Options

```text
c = create
x = extract
z = gzip
v = verbose
f = archive file
```

---

## 4.9 Networking

### Why?

Networking administration is required to understand connectivity, IP addresses, routes, ports, DNS, and communication between applications and servers.

### Important Commands

- `ip addr` / `ip a` — Displays network interfaces and IP addresses.
- `ip route` — Displays the system's routing table.
- `ip link` — Displays and manages network interfaces.
- `ss` — Displays sockets and listening network ports.
- `ping` — Tests basic network reachability using ICMP.
- `curl` — Makes network requests and is commonly used to test HTTP/HTTPS APIs.
- `wget` — Downloads files/resources from network locations.
- `nslookup` — Queries DNS information.
- `dig` — Performs detailed DNS queries when installed.
- `hostname` — Displays or manages the system hostname.
- `traceroute` — Shows the path packets take toward a destination when installed.

### Important Concepts

```text
IP address → Identifies a network interface/device.
Port       → Identifies a network service endpoint.
DNS        → Resolves domain names to IP addresses.
Route      → Determines where network traffic should go.
```

Common ports:

```text
22  → SSH
53  → DNS
80  → HTTP
443 → HTTPS
```

---

## 4.10 System Information

### Why?

System information commands help administrators understand the operating system, kernel, CPU, memory, storage, uptime, and hardware resources.

### Important Commands

- `uname -a` — Displays kernel and system information.
- `cat /etc/os-release` — Displays Linux distribution information.
- `hostname` — Displays the system hostname.
- `hostnamectl` — Displays or manages hostname/system information on systemd-based systems.
- `uptime` — Shows how long the system has been running and system load information.
- `lscpu` — Displays CPU architecture and processor information.
- `free -h` — Displays RAM and swap usage.
- `df -h` — Displays filesystem disk usage.
- `du -sh` — Displays disk usage of a file or directory.
- `lsblk` — Displays block devices and storage devices.
- `lsusb` — Displays connected USB devices.
- `lspci` — Displays PCI devices.
- `who` — Shows currently logged-in users.
- `w` — Shows logged-in users and what they are doing.

---

<img width="1601" height="811" alt="Screenshot 2026-08-24 180621" src="https://github.com/user-attachments/assets/efc47b03-59fe-4bdc-8a71-fb91d5c2258f" />
<img width="1649" height="647" alt="Screenshot 2026-08-24 180654" src="https://github.com/user-attachments/assets/69f25de7-1ac1-4d0b-88cb-03e91e452599" />
<img width="1678" height="755" alt="Screenshot 2026-08-24 180721" src="https://github.com/user-attachments/assets/539d1557-66c4-4336-8151-92de91e1e5df" />
<img width="1681" height="875" alt="Screenshot 2026-08-24 180803" src="https://github.com/user-attachments/assets/0f44cfc5-6bab-476f-b0bd-710d0ee8ccbf" />
<img width="1638" height="670" alt="Screenshot 2026-08-24 181036" src="https://github.com/user-attachments/assets/8da37288-f509-4e53-8e42-1bdf0ef175a7" />
<img width="1700" height="474" alt="Screenshot 2026-08-24 181056" src="https://github.com/user-attachments/assets/0bc6243a-a2cf-48f1-92e8-f3d61d83a2f4" />
<img width="1694" height="511" alt="Screenshot 2026-08-24 181112" src="https://github.com/user-attachments/assets/e0b9de85-4b8d-44bf-80f1-929b0d9221e0" />
<img width="1437" height="134" alt="Screenshot 2026-08-24 181150" src="https://github.com/user-attachments/assets/421f530b-0bef-4cd8-98c9-6c14d4b0aaf8" />
<img width="1712" height="882" alt="Screenshot 2026-08-24 181215" src="https://github.com/user-attachments/assets/0268a02e-3853-4d15-8c7a-bb628f0e9761" />
<img width="1699" height="871" alt="Screenshot 2026-08-24 182052" src="https://github.com/user-attachments/assets/63b1f48a-3d07-458c-8f8b-a4f434849552" />
<img width="1571" height="698" alt="Screenshot 2026-08-24 182148" src="https://github.com/user-attachments/assets/ff049daf-c93f-4f08-8f45-e294b8fc8063" />
<img width="1644" height="367" alt="Screenshot 2026-08-24 182159" src="https://github.com/user-attachments/assets/c9ae2304-2924-42a0-804a-4a7b5367cef5" />

#### Text processing:

<img width="1717" height="726" alt="Screenshot 2026-08-25 183214" src="https://github.com/user-attachments/assets/89ff9ca4-5bf0-46e2-aaf9-fe7f1fd75335" />
<img width="1698" height="788" alt="Screenshot 2026-08-25 183254" src="https://github.com/user-attachments/assets/4d0f3d9f-59e6-48cb-9368-4efb806e5e57" />
<img width="1711" height="730" alt="Screenshot 2026-08-25 183319" src="https://github.com/user-attachments/assets/3387334a-3ac2-4aca-9003-843e91955023" />

<img width="1702" height="647" alt="Screenshot 2026-08-26 121756" src="https://github.com/user-attachments/assets/7a05fb76-2dd0-4d1e-b7f5-e4c1018b282d" />
<img width="1533" height="488" alt="Screenshot 2026-08-26 121827" src="https://github.com/user-attachments/assets/51422ecd-a8c4-4427-9ab5-e92357519d94" />
<img width="1704" height="347" alt="Screenshot 2026-08-26 121852" src="https://github.com/user-attachments/assets/a4200e68-eb1d-4637-84ce-b9b3c247ae9a" />
<img width="1651" height="679" alt="Screenshot 2026-08-26 121953" src="https://github.com/user-attachments/assets/aa12d290-9a70-408f-aaa0-5900a8e27c13" />
<img width="1714" height="602" alt="Screenshot 2026-08-26 122048" src="https://github.com/user-attachments/assets/fba90e36-9cc1-490b-a603-793e6b72e253" />
<img width="1697" height="539" alt="Screenshot 2026-08-26 122119" src="https://github.com/user-attachments/assets/2c227af4-6253-4000-9549-342dc4a309f2" />
<img width="1367" height="346" alt="Screenshot 2026-08-26 122137" src="https://github.com/user-attachments/assets/ac2b44e6-0249-4781-b433-d8e415b025ee" />
<img width="1699" height="589" alt="Screenshot 2026-08-26 122159" src="https://github.com/user-attachments/assets/4d123245-7a64-414f-a701-57a1a7d0f602" />
<img width="1709" height="156" alt="Screenshot 2026-08-26 122624" src="https://github.com/user-attachments/assets/ec4d8351-6a9e-4769-ab62-ec7eb013dea4" />
<img width="1719" height="132" alt="Screenshot 2026-08-26 122648" src="https://github.com/user-attachments/assets/cd1242a7-fa49-4a22-a888-61a5cb005310" />
<img width="1711" height="134" alt="Screenshot 2026-08-26 122712" src="https://github.com/user-attachments/assets/7b366348-e4f1-46fb-87b4-38f40bc1281c" />
<img width="1689" height="188" alt="Screenshot 2026-08-26 122738" src="https://github.com/user-attachments/assets/72325ab7-5a4d-4883-854a-2a096eaff98c" />
<img width="1879" height="294" alt="Screenshot 2026-08-26 175046" src="https://github.com/user-attachments/assets/542da7d9-5a50-4171-83c2-bfcb5f6d04f9" />
<img width="1863" height="360" alt="Screenshot 2026-08-26 175101" src="https://github.com/user-attachments/assets/816f0392-0dd1-44b2-b8ca-ed18efb59bfd" />
<img width="1713" height="314" alt="Screenshot 2026-08-26 175521" src="https://github.com/user-attachments/assets/58d56489-480f-445a-a645-ddc42bdafa52" />
<img width="1899" height="811" alt="Screenshot 2026-08-26 175544" src="https://github.com/user-attachments/assets/230fb324-b8c7-444f-bffd-6b4826b63c2c" />
<img width="1899" height="912" alt="Screenshot 2026-08-26 175600" src="https://github.com/user-attachments/assets/6cba6f99-bbce-4551-a6f7-3d65c9a05980" />
<img width="1907" height="583" alt="Screenshot 2026-08-26 175620" src="https://github.com/user-attachments/assets/55dec937-09ea-4550-83e5-c24cb511bb2e" />
<img width="1905" height="847" alt="Screenshot 2026-08-26 175639" src="https://github.com/user-attachments/assets/17680957-5e7e-4eca-8a3f-629dfd3f48f8" />
<img width="1914" height="809" alt="Screenshot 2026-08-26 175656" src="https://github.com/user-attachments/assets/0e4a9e9d-283d-4da4-8054-1871a7dfe4ed" />
