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

---

## 2026-06-24 — Part 3: Web server package check

### Goal

Check whether Apache/httpd is installed on the RHEL server and verify whether the system can access repositories to install the web server package if needed.

This part confirms the current web server readiness state before attempting any service configuration.

### Work completed

* Checked whether the `httpd` package was installed.
* Checked whether the `httpd` command existed in the system path.
* Checked whether the `httpd` systemd service existed.
* Checked whether package information for `httpd` could be retrieved with `dnf`.
* Checked repository availability with `dnf repolist`.
* Attempted to install the `httpd` package.
* Confirmed that Apache/httpd could not be installed because the RHEL system is not registered and has no enabled repositories.
* Documented the package and repository limitation.
* Saved screenshot evidence of the package check and installation attempt.

### Verification results

| Item                         | Result                                                         |
| ---------------------------- | -------------------------------------------------------------- |
| `httpd` package status       | Not installed                                                  |
| `httpd` command availability | Not found                                                      |
| `httpd.service` status       | Unit could not be found                                        |
| `dnf info httpd`             | Failed / no matching package information available             |
| Repository status            | No repositories available                                      |
| Subscription status          | System not registered with an entitlement server               |
| `httpd` installation attempt | Failed                                                         |
| Reason installation failed   | No enabled repositories                                        |
| Web server configuration     | Not completed due to missing package and repository limitation |

### Commands used

```bash
rpm -q httpd
which httpd
systemctl status httpd --no-pager
sudo dnf info httpd
sudo dnf repolist
sudo dnf install -y httpd
```

### Command purpose

| Command                             | Purpose                                                                         |
| ----------------------------------- | ------------------------------------------------------------------------------- |
| `rpm -q httpd`                      | Checks whether the Apache/httpd package is installed.                           |
| `which httpd`                       | Checks whether the `httpd` command exists in the system path.                   |
| `systemctl status httpd --no-pager` | Checks whether the `httpd` service exists and whether it is running.            |
| `sudo dnf info httpd`               | Attempts to retrieve package information for `httpd` from enabled repositories. |
| `sudo dnf repolist`                 | Lists enabled software repositories.                                            |
| `sudo dnf install -y httpd`         | Attempts to install Apache/httpd without interactive confirmation.              |

### Notes

Apache/httpd was not installed on the server.

The `httpd` command was not found, and `systemctl` reported that `httpd.service` could not be found. This confirms that the Apache service is not currently available on the system.

The package lookup with `dnf info httpd` failed because the system could not access package information.

The repository check confirmed that no repositories are available. The installation attempt failed because the RHEL system is not registered with a Red Hat entitlement server and has no enabled repositories.

Because Apache/httpd could not be installed, normal web server setup cannot continue on this system until repository access is fixed.

This is a realistic system administration limitation. Future remediation would require registering the RHEL system with Red Hat subscription management or enabling a valid repository source before installing Apache/httpd.

This part demonstrates package verification, service readiness checking, repository troubleshooting and documentation of installation blockers.

### Evidence

Screenshot:

![screenshot-03-rhel-httpd-package-check.png](screenshots/screenshot-03-rhel-httpd-package-check.png)

---

## 2026-06-24 — Part 4: Web service readiness and repository limitation review

### Goal

Review the system’s repository readiness and web service readiness after confirming that Apache/httpd is not installed.

This part checks whether repository configuration exists, whether the system is registered with Red Hat subscription management, whether any repositories are available, whether alternative web server packages are installed, whether Python 3 is available for temporary lab testing, and whether any common web ports are already listening.

### Work completed

* Checked repository configuration under `/etc/yum.repos.d/`.
* Confirmed that `redhat.repo` exists.
* Checked additional repository paths referenced by DNF error output.
* Checked Red Hat subscription status.
* Confirmed that the system is not registered.
* Checked all DNF repository availability with `dnf repolist --all`.
* Confirmed that no repositories are available.
* Checked whether Nginx is installed.
* Checked whether Lighttpd is installed.
* Checked whether Python 3 is installed.
* Verified the Python 3 command path.
* Checked whether any services were listening on common web ports `80`, `443` or `8080`.
* Saved screenshot evidence of repository readiness and web service readiness.

### Verification results

| Item                         | Result                                                       |
| ---------------------------- | ------------------------------------------------------------ |
| `/etc/yum.repos.d/`          | Contains `redhat.repo`                                       |
| `/etc/distro.repos.d/`       | No visible output / not available in checked command output  |
| `/etc/yum/repos.d/`          | No visible output / not available in checked command output  |
| Subscription status          | Not registered                                               |
| `dnf repolist --all`         | No repositories available                                    |
| Nginx package status         | Not installed                                                |
| Lighttpd package status      | Not installed                                                |
| Python 3 package status      | Installed                                                    |
| Python 3 version             | `python3-3.12.11-3.el10.x86_64`                              |
| Python 3 path                | `/usr/bin/python3`                                           |
| Listening on port 80         | No matching listener shown                                   |
| Listening on port 443        | No matching listener shown                                   |
| Listening on port 8080       | No matching listener shown                                   |
| Web service setup readiness  | Blocked for Apache/httpd due to missing package repositories |
| Temporary lab testing option | Python 3 is available                                        |

### Commands used

```bash
ls -l /etc/yum.repos.d/
ls -l /etc/distro.repos.d/ 2>/dev/null
ls -l /etc/yum/repos.d/ 2>/dev/null
sudo subscription-manager status
sudo dnf repolist --all

rpm -q nginx
rpm -q lighttpd
rpm -q python3
which python3
ss -tulpen | grep -E ':80|:443|:8080' || true
```

### Command purpose

| Command                                              | Purpose                                                                                 |
| ---------------------------------------------------- | --------------------------------------------------------------------------------------- |
| `ls -l /etc/yum.repos.d/`                            | Lists repository configuration files in the standard RHEL/YUM/DNF repository directory. |
| `ls -l /etc/distro.repos.d/ 2>/dev/null`             | Checks an additional repository path while hiding missing-directory errors.             |
| `ls -l /etc/yum/repos.d/ 2>/dev/null`                | Checks another possible repository path while hiding missing-directory errors.          |
| `sudo subscription-manager status`                   | Checks whether the RHEL system is registered with Red Hat subscription management.      |
| `sudo dnf repolist --all`                            | Lists all known repositories, including disabled repositories.                          |
| `rpm -q nginx`                                       | Checks whether Nginx is installed.                                                      |
| `rpm -q lighttpd`                                    | Checks whether Lighttpd is installed.                                                   |
| `rpm -q python3`                                     | Checks whether Python 3 is installed.                                                   |
| `which python3`                                      | Shows the executable path for Python 3 if available.                                    |
| `ss -tulpen \| grep -E ':80\|:443\|:8080' \|\| true` | Checks whether any service is listening on common web ports 80, 443 or 8080.            |

### Notes

The repository readiness check showed that `/etc/yum.repos.d/` contains a `redhat.repo` file. However, the system is not registered with Red Hat subscription management, and DNF reports that no repositories are available.

This means package installation through DNF is still blocked, even though a repository file exists.

The web service readiness check showed that Nginx and Lighttpd are not installed. Python 3 is installed and available at `/usr/bin/python3`.

The command checking ports `80`, `443` and `8080` returned no matching output. This means no service was shown listening on those common web ports at the time of testing.

An accidental command typo, `rpm -l python3`, returned an unknown option error. The command was corrected to `rpm -q python3`, which confirmed that Python 3 is installed. This correction was kept as part of the evidence because it shows normal troubleshooting during command-line work.

Because Apache/httpd, Nginx and Lighttpd are not installed, the lab cannot continue as a normal installed web server service configuration on this RHEL system.

The lab can still continue with temporary Python-based web testing in later parts. This will be documented clearly as a lab testing method, not a production web server replacement.

### Evidence

Screenshots:

![screenshot-04a-rhel-repository-readiness.png](screenshots/screenshot-04a-rhel-repository-readiness.png)

![screenshot-04b-rhel-web-service-readiness.png](screenshots/screenshot-04b-rhel-web-service-readiness.png)

---

## 2026-06-24 — Part 5: Temporary web content and Python HTTP server test

### Goal

Create temporary static web content and test local web serving with Python 3.

Because Apache/httpd could not be installed due to repository and subscription limitations, this part uses Python’s built-in HTTP server as a temporary lab testing method.

This is not a production web server replacement. It is used only to verify basic static web content and local HTTP access.

### Work completed

* Created a temporary web content folder under the `vulkan` user home directory.
* Created an `index.html` file for the lab web page.
* Verified that `index.html` exists.
* Verified the contents of `index.html`.
* Started Python’s built-in HTTP server on port `8080`.
* Opened a second SSH terminal for testing.
* Used `curl` to request the local web page from `127.0.0.1:8080`.
* Confirmed that the HTML page was returned successfully.
* Verified that Python was listening on port `8080`.
* Stopped the temporary Python HTTP server.
* Confirmed that the temporary server test was successful.
* Saved screenshot evidence of the web content and Python HTTP server test.

### Verification results

| Item                       | Result                          |
| -------------------------- | ------------------------------- |
| Temporary web folder       | `/home/vulkan/web-test`         |
| Web page file              | `index.html`                    |
| Web content creation       | Successful                      |
| Temporary server command   | `python3 -m http.server 8080`   |
| Test URL                   | `http://127.0.0.1:8080`         |
| Local curl test            | Successful                      |
| Returned content           | HTML page displayed in terminal |
| Listening port during test | `0.0.0.0:8080`                  |
| Listening process          | `python3`                       |
| Production web server used | No                              |
| Temporary lab test used    | Yes                             |

### Commands used

```bash
mkdir -p ~/web-test
cd ~/web-test

cat > index.html <<'EOF'
<!DOCTYPE html>
<html>
<head>
    <title>RHEL Web Server Operations Lab</title>
</head>
<body>
    <h1>RHEL Web Server Operations Lab</h1>
    <p>This page is being served temporarily with Python 3 for lab testing.</p>
    <p>Apache/httpd could not be installed because the RHEL system is not registered and has no enabled repositories.</p>
    <p>Documentation identity: Vulkan</p>
</body>
</html>
EOF

ls -l index.html
cat index.html

python3 -m http.server 8080
curl http://127.0.0.1:8080
ss -tulpen | grep ':8080'
ss -tulpen | grep ':8080' || true
```

### Command purpose

| Command                                | Purpose                                                                                  |
| -------------------------------------- | ---------------------------------------------------------------------------------------- |
| `mkdir -p ~/web-test`                  | Creates the temporary web content folder if it does not already exist.                   |
| `cd ~/web-test`                        | Moves into the temporary web content folder.                                             |
| `cat > index.html <<'EOF'`             | Creates the `index.html` file using heredoc input.                                       |
| `ls -l index.html`                     | Confirms that the web page file exists and shows permissions, owner, size and timestamp. |
| `cat index.html`                       | Displays the HTML file contents for verification.                                        |
| `python3 -m http.server 8080`          | Starts Python’s temporary HTTP server on port `8080`.                                    |
| `curl http://127.0.0.1:8080`           | Sends a local HTTP request to the temporary web server.                                  |
| `ss -tulpen \| grep ':8080'`           | Confirms that a process is listening on port `8080`.                                     |
| `ss -tulpen \| grep ':8080' \|\| true` | Checks whether port `8080` is still listening after the server is stopped.               |

### Notes

The `nano` text editor was not installed on the system, so the HTML file was created using a heredoc with `cat`.

This was appropriate because package installation is currently blocked by the system’s missing repository and subscription configuration.

The temporary Python HTTP server successfully served the static HTML page from `/home/vulkan/web-test`.

The `curl` test confirmed that the page was reachable locally through `http://127.0.0.1:8080`.

The `ss` check confirmed that Python was listening on `0.0.0.0:8080` during the test.

Python’s built-in HTTP server was used only as a temporary lab testing tool. It is not suitable as a production replacement for Apache/httpd.

This part demonstrates static content creation, temporary web service testing, local HTTP testing and listening port verification despite the Apache installation limitation.

### Evidence

Screenshots:

![screenshot-05a-rhel-temporary-web-content.png](screenshots/screenshot-05a-rhel-temporary-web-content.png)

![screenshot-05b-rhel-python-http-server-test.png](screenshots/screenshot-05b-rhel-python-http-server-test.png)

---

## 2026-06-25 — Part 6: Web file permissions

### Goal

Review and configure basic permissions for the temporary web content used in the lab.

Because Apache/httpd could not be installed, the lab used a temporary Python-based HTTP server. Even in this temporary setup, file permissions still matter because web content should be readable by the service process while write access remains limited to the owner.

### Work completed

* Reviewed permissions for the temporary web content folder.
* Reviewed permissions for `index.html`.
* Reviewed detailed metadata with `stat`.
* Set the web content folder permission mode to `755`.
* Set the `index.html` file permission mode to `644`.
* Verified ownership and permissions after the change.
* Verified SELinux context information shown by `stat`.
* Started the temporary Python HTTP server again after the permission change.
* Used `curl` to confirm that the web page still loaded successfully.
* Verified that Python was listening on port `8080`.
* Stopped the temporary Python server.
* Verified that port `8080` was no longer listening after the server stopped.
* Saved screenshot evidence of the permission review and service test.

### Verification results

| Item                          | Result                                 |
| ----------------------------- | -------------------------------------- |
| Web content folder            | `/home/vulkan/web-test`                |
| Web page file                 | `/home/vulkan/web-test/index.html`     |
| Folder owner/group            | `vulkan:vulkan`                        |
| File owner/group              | `vulkan:vulkan`                        |
| Folder permissions            | `0755 / drwxr-xr-x`                    |
| File permissions              | `0644 / -rw-r--r--`                    |
| Folder SELinux context        | `unconfined_u:object_r:user_home_t:s0` |
| File SELinux context          | `unconfined_u:object_r:user_home_t:s0` |
| Post-permission web test      | Successful                             |
| Test URL                      | `http://127.0.0.1:8080`                |
| Listening process during test | `python3`                              |
| Listening port during test    | `0.0.0.0:8080`                         |
| Port after stopping server    | No matching listener shown             |

### Commands used

```bash
cd ~/web-test
pwd

ls -ld ~/web-test
ls -l ~/web-test/index.html
stat ~/web-test
stat ~/web-test/index.html

chmod 755 ~/web-test
chmod 644 ~/web-test/index.html

ls -ld ~/web-test
ls -l ~/web-test/index.html
stat ~/web-test
stat ~/web-test/index.html

python3 -m http.server 8080
curl http://127.0.0.1:8080
ss -tulpen | grep ':8080'
ss -tulpen | grep ':8080' || true
```

### Command purpose

| Command                                | Purpose                                                                                           |
| -------------------------------------- | ------------------------------------------------------------------------------------------------- |
| `cd ~/web-test`                        | Moves into the temporary web content folder.                                                      |
| `pwd`                                  | Prints the current directory path for verification.                                               |
| `ls -ld ~/web-test`                    | Shows permissions, owner and group for the folder itself.                                         |
| `ls -l ~/web-test/index.html`          | Shows permissions, owner and group for the web page file.                                         |
| `stat ~/web-test`                      | Shows detailed metadata for the folder, including numeric permission mode and SELinux context.    |
| `stat ~/web-test/index.html`           | Shows detailed metadata for the HTML file, including numeric permission mode and SELinux context. |
| `chmod 755 ~/web-test`                 | Sets the folder so the owner can read/write/enter, while others can read and enter.               |
| `chmod 644 ~/web-test/index.html`      | Sets the HTML file so the owner can read/write, while others can read only.                       |
| `python3 -m http.server 8080`          | Starts Python’s temporary HTTP server on port `8080`.                                             |
| `curl http://127.0.0.1:8080`           | Sends a local HTTP request to confirm the page still loads.                                       |
| `ss -tulpen \| grep ':8080'`           | Confirms that Python is listening on port `8080`.                                                 |
| `ss -tulpen \| grep ':8080' \|\| true` | Checks whether port `8080` is still listening after stopping the server.                          |

### Notes

The temporary web content folder was configured with permission mode `0755`. This allows the owner to manage the folder while allowing read and execute access for others.

The `index.html` file was configured with permission mode `0644`. This allows the owner to edit the file while allowing others to read it.

These permissions are appropriate for basic static web content in a lab environment because the page can be read, but the content is not world-writable.

The `stat` output also showed the SELinux context `user_home_t` for both the folder and the HTML file. This will be useful in the next part when SELinux web context behavior is reviewed.

After changing permissions, the Python HTTP server was started again on port `8080`. The `curl` test confirmed that the page still loaded successfully.

The listening port check showed Python listening on `0.0.0.0:8080` during the test. After stopping the server, a final port check returned no matching listener.

This part demonstrates basic web file permission review, permission hardening, service validation and post-change testing.

### Evidence

Screenshots:

![screenshot-06a-rhel-web-file-permissions.png](screenshots/screenshot-06a-rhel-web-file-permissions.png)

![screenshot-06b-rhel-web-file-permissions.png](screenshots/screenshot-06b-rhel-web-file-permissions.png)

![screenshot-06c-rhel-web-permission-service-test.png](screenshots/screenshot-06c-rhel-web-permission-service-test.png)
---

## 2026-06-25 — Part 7: SELinux web context review

### Goal

Review SELinux status and SELinux contexts for the temporary web content used in the lab.

Because Apache/httpd could not be installed, the lab used temporary Python-based web testing. The web content was stored under `/home/vulkan/web-test`, so this part documents how SELinux labels the folder and file in that location.

### Work completed

* Verified that SELinux is enabled.
* Verified that SELinux is running in enforcing mode.
* Reviewed detailed SELinux status with `sestatus`.
* Reviewed SELinux context labels for the temporary web content folder.
* Reviewed SELinux context labels for `index.html`.
* Verified folder permissions and metadata with `stat`.
* Verified file permissions and metadata with `stat`.
* Checked whether any Python web server process was still running.
* Checked whether port `8080` was still listening.
* Saved screenshot evidence of the SELinux status and context review.

### Verification results

| Item                         | Result                                 |
| ---------------------------- | -------------------------------------- |
| SELinux status               | Enabled                                |
| Current SELinux mode         | Enforcing                              |
| Configured SELinux mode      | Enforcing                              |
| Loaded policy name           | `targeted`                             |
| Temporary web folder         | `/home/vulkan/web-test`                |
| Web page file                | `/home/vulkan/web-test/index.html`     |
| Folder SELinux context       | `unconfined_u:object_r:user_home_t:s0` |
| File SELinux context         | `unconfined_u:object_r:user_home_t:s0` |
| Folder permissions           | `0755 / drwxr-xr-x`                    |
| File permissions             | `0644 / -rw-r--r--`                    |
| Owner/group                  | `vulkan:vulkan`                        |
| Python HTTP server status    | No temporary lab server shown          |
| Port `8080` listener status  | No matching listener shown             |

### Commands used

```bash
getenforce
sestatus

cd ~/web-test
ls -Z
ls -Zd ~/web-test
ls -Z ~/web-test/index.html

stat ~/web-test
stat ~/web-test/index.html

ps -ef | grep '[p]ython3' || true
ss -tulpen | grep ':8080' || true
```

### Command purpose

| Command                                  | Purpose                                                                                      |
| ---------------------------------------- | -------------------------------------------------------------------------------------------- |
| `getenforce`                             | Shows the current SELinux mode.                                                              |
| `sestatus`                               | Shows detailed SELinux status, including policy name and configured mode.                    |
| `cd ~/web-test`                          | Moves into the temporary web content folder.                                                  |
| `ls -Z`                                  | Lists files in the current directory with SELinux context labels.                            |
| `ls -Zd ~/web-test`                      | Shows the SELinux context for the temporary web content folder itself.                       |
| `ls -Z ~/web-test/index.html`            | Shows the SELinux context for the HTML file.                                                  |
| `stat ~/web-test`                        | Shows detailed folder metadata, including permissions, owner, group and SELinux context.     |
| `stat ~/web-test/index.html`             | Shows detailed file metadata, including permissions, owner, group and SELinux context.       |
| `ps -ef \| grep '[p]ython3' \|\| true`   | Checks whether a Python process is running while avoiding a false match on the grep command. |
| `ss -tulpen \| grep ':8080' \|\| true`   | Checks whether anything is listening on TCP port `8080`.                                     |

### Notes

SELinux was enabled and running in enforcing mode.

The temporary web folder and `index.html` file were labeled with the SELinux context `user_home_t`. This is expected because the files are stored under the `vulkan` user home directory.

A normal Apache/httpd web root would usually use a web content context such as `httpd_sys_content_t`. Since Apache/httpd could not be installed, Apache-specific SELinux policy behavior could not be tested in this lab.

No SELinux policy changes or context changes were made in this part. The goal was to document the current SELinux state honestly.

The process check showed a Python-related process for firewalld, but this was not the temporary Python HTTP server. The port check showed that nothing was listening on port `8080`.

This part demonstrates SELinux status verification, SELinux file context review and security-aware documentation of a lab limitation.

### Evidence

Screenshots:

![screenshot-07a-rhel-selinux-status.png](screenshots/screenshot-07a-rhel-selinux-status.png)

![screenshot-07b-rhel-web-content-contexts.png](screenshots/screenshot-07b-rhel-web-content-contexts.png)

---

## 2026-06-25 — Part 8: Firewalld port 8080 test

### Goal

Review firewalld status and test temporary firewall access for TCP port `8080`.

Since Apache/httpd could not be installed, port `8080` was used for the Python temporary web server lab test. This part demonstrates how firewall access can be temporarily opened and then removed again.

### Work completed

* Verified that firewalld was running.
* Reviewed the active firewall zone.
* Reviewed the current firewalld configuration.
* Temporarily opened TCP port `8080`.
* Verified that `8080/tcp` appeared in the open port list.
* Removed TCP port `8080` after testing.
* Verified that `8080/tcp` was no longer listed.
* Documented that the firewall rule was not made permanent.
* Saved screenshot evidence of the before, added and removed firewall states.

### Verification results

| Item                              | Result                  |
| --------------------------------- | ----------------------- |
| Firewalld state                   | Running                 |
| Active zone                       | Reviewed                |
| Port added                        | `8080/tcp`              |
| Port add result                   | Successful              |
| Port list after adding            | Included `8080/tcp`     |
| Port removed                      | `8080/tcp`              |
| Port removal result               | Successful              |
| Port list after removal           | No `8080/tcp` shown     |
| Permanent firewall rule created   | No                      |

### Commands used

```bash
sudo firewall-cmd --state
sudo firewall-cmd --get-active-zones
sudo firewall-cmd --list-all

sudo firewall-cmd --add-port=8080/tcp
sudo firewall-cmd --list-ports

sudo firewall-cmd --remove-port=8080/tcp
sudo firewall-cmd --list-ports
```

### Command purpose

| Command                                      | Purpose                                                                           |
| -------------------------------------------- | --------------------------------------------------------------------------------- |
| `sudo firewall-cmd --state`                  | Checks whether firewalld is running.                                              |
| `sudo firewall-cmd --get-active-zones`       | Shows the active firewall zone and the network interface assigned to it.           |
| `sudo firewall-cmd --list-all`               | Shows the current firewalld configuration for the active/default zone.             |
| `sudo firewall-cmd --add-port=8080/tcp`      | Temporarily opens TCP port `8080` in firewalld.                                   |
| `sudo firewall-cmd --list-ports`             | Lists custom open ports in the current firewalld runtime configuration.            |
| `sudo firewall-cmd --remove-port=8080/tcp`   | Removes the temporary firewall opening for TCP port `8080`.                       |

### Notes

The firewall rule was not made permanent. This was intentional because the purpose was to demonstrate temporary firewall testing for the lab.

Opening port `8080/tcp` is relevant because the lab used Python's built-in HTTP server on port `8080` for temporary web testing.

After testing, port `8080/tcp` was removed again. The final `firewall-cmd --list-ports` check showed no `8080/tcp` entry.

A warning appeared when removing port `8080` a second time because the port had already been removed. This confirmed that the first removal had already succeeded and that the runtime firewall configuration no longer included the port.

This part demonstrates firewall status review, temporary port access control and safe cleanup after testing.

### Evidence

Screenshots:

![screenshot-08a-rhel-firewalld-before-port-8080.png](screenshots/screenshot-08a-rhel-firewalld-before-port-8080.png)

![screenshot-08b-rhel-firewalld-port-8080-added.png](screenshots/screenshot-08b-rhel-firewalld-port-8080-added.png)

![screenshot-08c-rhel-firewalld-port-8080-removed.png](screenshots/screenshot-08c-rhel-firewalld-port-8080-removed.png)
---

## 2026-06-25 — Part 9: Local and network testing

### Goal

Test the temporary Python web server from localhost, the RHEL server IP address and the Windows host machine.

This part verifies that the temporary web content can be reached locally and over the network when firewalld temporarily allows port `8080/tcp`.

### Work completed

* Temporarily opened TCP port `8080` in firewalld.
* Verified that `8080/tcp` appeared in the open port list.
* Started Python's built-in HTTP server from `/home/vulkan/web-test`.
* Tested local access from the RHEL server using `127.0.0.1`.
* Tested network access using the RHEL server IP address `192.168.80.134`.
* Tested access from the Windows host machine.
* Verified that Python was listening on port `8080`.
* Stopped the temporary Python HTTP server.
* Verified that port `8080` was no longer listening after cleanup.
* Removed the temporary firewalld rule for `8080/tcp`.
* Saved screenshot evidence of local, network and cleanup testing.

### Verification results

| Item                          | Result                              |
| ----------------------------- | ----------------------------------- |
| Temporary firewall port       | `8080/tcp`                          |
| Temporary server command      | `python3 -m http.server 8080`       |
| Localhost test                | Successful                          |
| RHEL server IP test           | Successful                          |
| Windows host test             | Successful                          |
| Listening port during test    | `0.0.0.0:8080`                      |
| Cleanup server status         | No matching listener shown          |
| Firewall cleanup              | `8080/tcp` removed                  |

### Commands used

```bash
sudo firewall-cmd --add-port=8080/tcp
sudo firewall-cmd --list-ports

cd ~/web-test
python3 -m http.server 8080

curl http://127.0.0.1:8080
curl http://192.168.80.134:8080
ss -tulpen | grep ':8080'

ss -tulpen | grep ':8080' || true
sudo firewall-cmd --remove-port=8080/tcp
sudo firewall-cmd --list-ports
```

Windows host test:

```powershell
Invoke-WebRequest http://192.168.80.134:8080 -UseBasicParsing
```

### Command purpose

| Command                                                        | Purpose                                                                    |
| -------------------------------------------------------------- | -------------------------------------------------------------------------- |
| `sudo firewall-cmd --add-port=8080/tcp`                        | Temporarily opens TCP port `8080` in firewalld.                            |
| `sudo firewall-cmd --list-ports`                               | Lists custom open ports in firewalld.                                      |
| `cd ~/web-test`                                                | Moves into the temporary web content folder.                               |
| `python3 -m http.server 8080`                                  | Starts Python's temporary HTTP server on port `8080`.                      |
| `curl http://127.0.0.1:8080`                                   | Tests web access from the RHEL server using localhost.                     |
| `curl http://192.168.80.134:8080`                              | Tests web access using the RHEL server IP address.                         |
| `ss -tulpen \| grep ':8080'`                                   | Confirms that Python is listening on port `8080`.                          |
| `ss -tulpen \| grep ':8080' \|\| true`                         | Confirms that port `8080` is no longer listening after server cleanup.     |
| `sudo firewall-cmd --remove-port=8080/tcp`                     | Removes the temporary firewall opening for port `8080`.                    |
| `Invoke-WebRequest http://192.168.80.134:8080 -UseBasicParsing` | Tests web access from Windows to the RHEL server without script parsing.   |

### Notes

The local test with `127.0.0.1` verifies access from the RHEL server itself.

The test with `192.168.80.134` verifies access through the server's network interface.

The Windows host test verifies that another machine can reach the temporary web page over the network when firewalld allows port `8080/tcp`.

The Python server was stopped after testing, and the temporary firewall opening was removed. This kept the lab system in a clean post-test state.

### Evidence

Screenshots:

![screenshot-09a-rhel-local-and-ip-web-test.png](screenshots/screenshot-09a-rhel-local-and-ip-web-test.png)

![screenshot-09b-windows-browser-web-test.png](screenshots/screenshot-09b-windows-browser-web-test.png)

![screenshot-09c-rhel-web-test-cleanup.png](screenshots/screenshot-09c-rhel-web-test-cleanup.png)

---

## 2026-06-25 — Part 10: Web server log review

### Goal

Review web request logging for the temporary Python HTTP server and check whether Apache/httpd logs are available.

Because Apache/httpd could not be installed, this part documents the difference between Python's terminal-based request logs and normal Apache/httpd log files.

### Work completed

* Temporarily opened port `8080/tcp` for testing.
* Started Python's built-in HTTP server on port `8080`.
* Generated web requests from RHEL and Windows.
* Verified that Python logged requests in the terminal.
* Confirmed successful HTTP `200 OK` responses.
* Checked whether `/var/log/httpd` was available.
* Confirmed that Apache/httpd was not installed.
* Searched system logs with `journalctl`.
* Stopped the temporary Python server.
* Verified cleanup of port `8080`.
* Removed the temporary firewalld rule.
* Saved screenshot evidence of request logs, Windows request success and cleanup.

### Verification results

| Item                         | Result                                      |
| ---------------------------- | ------------------------------------------- |
| Python request logging        | Visible in the server terminal              |
| Successful request pattern    | `GET / HTTP/1.1` with status `200`          |
| Windows request result        | `StatusCode: 200` / `StatusDescription: OK` |
| Apache/httpd log directory    | Not available                               |
| Apache/httpd package status   | Not installed                               |
| System log search             | Completed with `journalctl`                 |
| Cleanup state                 | Server stopped and port removed             |

### Commands used

```bash
sudo firewall-cmd --add-port=8080/tcp
sudo firewall-cmd --list-ports

cd ~/web-test
python3 -m http.server 8080

curl http://127.0.0.1:8080
curl http://192.168.80.134:8080

ls -l /var/log/httpd 2>/dev/null || echo "Apache/httpd log directory not available"
rpm -q httpd

journalctl --since "today" --no-pager | grep -i python || true
journalctl --since "today" --no-pager | grep -i http || true
journalctl --since "today" --no-pager | grep -i firewall || true

ss -tulpen | grep ':8080' || true
sudo firewall-cmd --remove-port=8080/tcp
sudo firewall-cmd --list-ports
```

Windows host test:

```powershell
Invoke-WebRequest http://192.168.80.134:8080 -UseBasicParsing
```

### Command purpose

| Command                                                        | Purpose                                                                   |
| -------------------------------------------------------------- | ------------------------------------------------------------------------- |
| `python3 -m http.server 8080`                                  | Starts the temporary Python HTTP server and prints request logs.          |
| `curl http://127.0.0.1:8080`                                   | Generates a local request to the temporary web server.                    |
| `curl http://192.168.80.134:8080`                              | Generates a request using the RHEL server IP address.                     |
| `Invoke-WebRequest http://192.168.80.134:8080 -UseBasicParsing` | Generates a Windows host request to the RHEL web server.                  |
| `ls -l /var/log/httpd 2>/dev/null \|\| echo ...`                | Checks for the Apache/httpd log directory and prints a fallback message.  |
| `rpm -q httpd`                                                 | Confirms whether Apache/httpd is installed.                               |
| `journalctl --since "today" --no-pager`                       | Reads system journal entries from the current day.                        |
| `grep -i python`, `grep -i http`, `grep -i firewall`            | Filters journal output for relevant log terms.                            |
| `ss -tulpen \| grep ':8080' \|\| true`                         | Verifies whether anything is still listening on port `8080`.              |
| `sudo firewall-cmd --remove-port=8080/tcp`                     | Removes the temporary firewall opening for port `8080`.                   |

### Notes

Python's built-in HTTP server wrote request logs directly to the terminal where it was running. This provided visible request evidence such as successful `GET /` requests returning `200`.

A Windows PowerShell request returned `StatusCode: 200` and `StatusDescription: OK`, confirming successful access from the host machine.

Apache/httpd logs were not available because Apache/httpd was not installed. This is expected based on the earlier package and repository limitation.

The system journal was searched for Python, HTTP and firewall-related entries. This demonstrated general system log review even though no Apache-specific logs were available.

### Evidence

Screenshots:

![screenshot-10a-rhel-python-web-request-logs.png](screenshots/screenshot-10a-rhel-python-web-request-logs.png)

![screenshot-10b-windows-web-request-success.png](screenshots/screenshot-10b-windows-web-request-success.png)

![screenshot-10c-rhel-log-review-cleanup.png](screenshots/screenshot-10c-rhel-log-review-cleanup.png)

---

## 2026-06-25 — Part 11: Troubleshooting reflection

### Goal

Create a troubleshooting reflection document that summarizes the main issues, limitations, workarounds and future remediation steps from the RHEL Web Server Operations Lab.

### Work completed

* Created `docs/troubleshooting_reflection.md`.
* Documented that Apache/httpd could not be installed.
* Documented that the RHEL system is not registered and has no enabled repositories.
* Documented that Python 3 was used as a temporary fallback for static web testing.
* Documented the unavailable `nano` editor and the heredoc workaround with `cat`.
* Documented file permission findings.
* Documented SELinux context findings.
* Documented firewalld port `8080` testing.
* Documented local, network and Windows host web testing.
* Documented Python HTTP server request logging.
* Documented production limitations.
* Documented future remediation steps for a proper Apache/httpd setup.
* Saved screenshot evidence of the troubleshooting reflection document.

### Files created

```text
docs/troubleshooting_reflection.md
```

### Notes

The troubleshooting reflection explains why the lab could not continue as a normal Apache/httpd installation and configuration project.

Instead of ignoring the repository and subscription limitation, the project documents the blocker clearly and uses temporary Python-based web testing to demonstrate useful sysadmin verification skills.

This part improves the project by showing realistic troubleshooting, limitation handling and professional documentation.

### Evidence

Screenshot:

![screenshot-11a-troubleshooting-reflection-document.png](screenshots/screenshot-11a-troubleshooting-reflection-document.png)

