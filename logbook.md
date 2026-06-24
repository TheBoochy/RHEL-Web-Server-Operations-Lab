# RHEL Web Server Operations Lab — Logbook

## 2026-06-24 — Part 1: Repository setup and planning

### Goal

Start the RHEL Web Server Operations Lab by creating the local project structure, initial documentation files and Git repository.

### Work completed

* Created the local project folder.

* Created the main documentation folders:

  * docs
  * screenshots
  * scripts
  * results

* Created `README.md`.

* Created `logbook.md`.

* Created `.gitkeep` files so Git can track empty folders.

* Initialized the local Git repository.

* Verified the initial Git status.

* Prepared the project for the first commit.

* Created the GitHub repository.

* Connected the local repository to GitHub.

* Pushed the initial project structure to GitHub.

### Project structure

```text
RHEL-Web-Server-Operations-Lab/
├── docs/
│   └── .gitkeep
├── results/
│   └── .gitkeep
├── screenshots/
│   ├── .gitkeep
│   └── screenshot-01-project-structure-and-git-status.png
├── scripts/
│   └── .gitkeep
├── logbook.md
└── README.md
```

### Commands used

```powershell
cd C:\Users\rband
mkdir RHEL-Web-Server-Operations-Lab
cd RHEL-Web-Server-Operations-Lab

mkdir docs
mkdir screenshots
mkdir scripts
mkdir results

New-Item README.md
New-Item logbook.md

New-Item docs\.gitkeep
New-Item screenshots\.gitkeep
New-Item scripts\.gitkeep
New-Item results\.gitkeep

git init
git status
git add .
git commit -m "Initial project structure"
git remote add origin https://github.com/TheBoochy/RHEL-Web-Server-Operations-Lab.git
git branch -M main
git push -u origin main
git status
```

### Command purpose

| Command                                     | Purpose                                                               |
| ------------------------------------------- | --------------------------------------------------------------------- |
| `cd C:\Users\rband`                         | Moves PowerShell to the user folder.                                  |
| `mkdir RHEL-Web-Server-Operations-Lab`      | Creates the main project folder.                                      |
| `cd RHEL-Web-Server-Operations-Lab`         | Moves into the project folder.                                        |
| `mkdir docs`                                | Creates the documentation folder.                                     |
| `mkdir screenshots`                         | Creates the screenshot evidence folder.                               |
| `mkdir scripts`                             | Creates the script storage folder.                                    |
| `mkdir results`                             | Creates the command output and result storage folder.                 |
| `New-Item README.md`                        | Creates the main project README file.                                 |
| `New-Item logbook.md`                       | Creates the project logbook file.                                     |
| `New-Item .gitkeep`                         | Creates placeholder files so Git tracks empty folders.                |
| `git init`                                  | Initializes a local Git repository.                                   |
| `git status`                                | Shows repository status and untracked files.                          |
| `git add .`                                 | Stages all project files for commit.                                  |
| `git commit -m "Initial project structure"` | Creates the first local Git commit.                                   |
| `git remote add origin`                     | Connects the local repository to the GitHub repository.               |
| `git branch -M main`                        | Renames the current branch to `main`.                                 |
| `git push -u origin main`                   | Uploads the local `main` branch to GitHub and sets upstream tracking. |

### Notes

Git does not track empty folders by default, so `.gitkeep` files were added to the main project folders.

The first push initially failed because the GitHub repository had not been created yet. After the GitHub repository was created, the initial commit was pushed successfully.

This part prepares the project structure and documentation base for the rest of the lab.

The project will continue with RHEL baseline verification before any web server configuration is attempted.

### Evidence

Screenshot:

![screenshot-01-project-structure-and-git-status.png](screenshots/screenshot-01-project-structure-and-git-status.png)

---

## 2026-06-24 — Part 2: RHEL server baseline verification

### Goal

Verify the current Red Hat Enterprise Linux server baseline before checking or configuring any web server services.

This baseline confirms the hostname, operating system, network configuration, disk usage, memory usage, SELinux mode and firewalld status.

### Work completed

* Verified the server hostname and system information.
* Verified the currently logged-in user.
* Verified the installed Red Hat Enterprise Linux version.
* Reviewed network interfaces and IP address information.
* Reviewed disk usage.
* Reviewed memory and swap usage.
* Verified SELinux mode.
* Verified firewalld service status.
* Saved screenshot evidence of the baseline verification.

### Commands used

```bash
hostnamectl
whoami
cat /etc/os-release
ip addr
df -h
free -h
getenforce
sudo systemctl status firewalld --no-pager
```

### Command purpose

| Command                                      | Purpose                                                                                |
| -------------------------------------------- | -------------------------------------------------------------------------------------- |
| `hostnamectl`                                | Shows hostname, operating system, kernel, architecture and virtualization information. |
| `whoami`                                     | Shows the currently logged-in user.                                                    |
| `cat /etc/os-release`                        | Displays the installed Linux distribution and version details.                         |
| `ip addr`                                    | Shows network interfaces, MAC addresses and IP addresses.                              |
| `df -h`                                      | Shows filesystem disk usage in human-readable format.                                  |
| `free -h`                                    | Shows memory and swap usage in human-readable format.                                  |
| `getenforce`                                 | Shows the current SELinux mode.                                                        |
| `sudo systemctl status firewalld --no-pager` | Shows whether the firewalld service is loaded, enabled and running.                    |

### Notes

The server baseline was verified before any web server package checks or service configuration.

This step is important because it provides a known starting point for the rest of the lab. If later web service, firewall or SELinux behavior changes, the baseline can be used for comparison.

SELinux and firewalld are especially important for this lab because web server access can be affected by both normal Linux configuration and security controls.

### Evidence

Screenshots:

![screenshot-02a-rhel-baseline-system.png](screenshots/screenshot-02a-rhel-baseline-system.png)

![screenshot-02b-rhel-baseline-security-and-resources.png](screenshots/screenshot-02b-rhel-baseline-security-and-resources.png)
