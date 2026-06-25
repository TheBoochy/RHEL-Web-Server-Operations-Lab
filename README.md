# RHEL Web Server Operations Lab

## Overview

RHEL Web Server Operations Lab is a voluntary sysadmin portfolio project focused on basic Red Hat Enterprise Linux web server administration and web service readiness checks.

The lab is designed to practice service management, package checks, repository troubleshooting, service readiness review, temporary web testing, file permissions, SELinux review, firewalld configuration, log review and documentation.

Public documentation uses the name **Vulkan**.

---

## Scenario

A small organization needs a basic internal web server hosted on Red Hat Enterprise Linux.

The goal of this lab is to configure, verify and document a simple RHEL-based web service environment using a structured sysadmin workflow.

During the lab, the Apache/httpd package was checked and confirmed to be unavailable on the current system because the RHEL server is not registered and has no enabled repositories. This limitation is documented as part of the troubleshooting process.

Because Apache/httpd could not be installed, the lab continued with temporary Python-based web testing to validate basic static web content, file permissions, SELinux context information, firewall access behavior and local web access.

---

## Lab goals

The goals of this lab are to:

* Create a clean Red Hat-focused web server project.
* Verify the RHEL server baseline.
* Check whether Apache/httpd is installed or available.
* Review package and repository readiness.
* Document missing package and repository limitations.
* Check whether alternative web server tools are installed.
* Verify whether Python 3 is available for temporary lab-based web testing.
* Create temporary static web content.
* Test local web serving with Python 3 on port 8080.
* Review and configure basic web file permissions.
* Review SELinux status and file contexts.
* Review and test firewalld access where possible.
* Test local and network readiness where possible.
* Review service and system logs.
* Document each part with screenshots and Git commits.

---

## Planned parts

| Part    | Topic                                                  | Status   |
| ------- | ------------------------------------------------------ | -------- |
| Part 1  | Repository setup and planning                          | Complete |
| Part 2  | RHEL server baseline verification                      | Complete |
| Part 3  | Web server package check                               | Complete |
| Part 4  | Web service readiness and repository limitation review | Complete |
| Part 5  | Temporary web content and Python HTTP server test      | Complete |
| Part 6  | Web file permissions                                   | Complete |
| Part 7  | SELinux web context review                             | Complete |
| Part 8  | Firewalld HTTP access                                  | Complete |
| Part 9  | Local and network testing                              | Complete |
| Part 10 | Web server log review                                  | Complete |
| Part 11 | Troubleshooting reflection                             | Complete |
| Part 12 | Final README and GitHub polish                         | Planned  |

---

## Project structure

```text
RHEL-Web-Server-Operations-Lab/
├── docs/
│   ├── .gitkeep
│   └── troubleshooting_reflection.md
├── results/
│   └── .gitkeep
├── screenshots/
│   ├── .gitkeep
│   ├── screenshot-01-project-structure-and-git-status.png
│   ├── screenshot-02a-rhel-baseline-system.png
│   ├── screenshot-02b-rhel-baseline-security-and-resources.png
│   ├── screenshot-03-rhel-httpd-package-check.png
│   ├── screenshot-04a-rhel-repository-readiness.png
│   ├── screenshot-04b-rhel-web-service-readiness.png
│   ├── screenshot-05a-rhel-temporary-web-content.png
│   ├── screenshot-05b-rhel-python-http-server-test.png
│   ├── screenshot-06a-rhel-web-file-permissions.png
│   ├── screenshot-06b-rhel-web-file-permissions.png
│   ├── screenshot-06c-rhel-web-permission-service-test.png
│   ├── screenshot-07a-rhel-selinux-status.png
│   ├── screenshot-07b-rhel-web-content-contexts.png
│   ├── screenshot-08a-rhel-firewalld-before-port-8080.png
│   ├── screenshot-08b-rhel-firewalld-port-8080-added.png
│   ├── screenshot-08c-rhel-firewalld-port-8080-removed.png
│   ├── screenshot-09a-rhel-local-and-ip-web-test.png
│   ├── screenshot-09b-windows-browser-web-test.png
│   ├── screenshot-09c-rhel-web-test-cleanup.png
│   ├── screenshot-10a-rhel-python-web-request-logs.png
│   ├── screenshot-10b-windows-web-request-success.png
│   ├── screenshot-10c-rhel-log-review-cleanup.png
│   └── screenshot-11a-troubleshooting-reflection-document.png
├── scripts/
│   └── .gitkeep
├── logbook.md
└── README.md
```


## Current progress

The project currently has the initial repository structure completed, the RHEL server baseline verified, the web server package check completed, the web service readiness limitation reviewed, a temporary Python-based web server test completed, web file permissions reviewed, SELinux web content contexts documented, temporary firewalld port access tested, local and network access verified, web request logging reviewed and a troubleshooting reflection document created.

The baseline verification confirms the server identity, operating system, network configuration, disk usage, memory usage, SELinux mode and firewalld status before any web server package checks or configuration changes are made.

The web server package check confirmed that Apache/httpd is not installed. The `httpd` command and `httpd.service` were not found. Package lookup and installation attempts failed because the RHEL system is not registered with an entitlement server and has no enabled repositories.

The repository readiness review confirmed that a `redhat.repo` file exists, but the system is not registered and DNF reports no usable repositories. The web service readiness check confirmed that Nginx and Lighttpd are not installed, while Python 3 is available. No services were listening on common web ports `80`, `443` or `8080` before testing.

Temporary web content was created in `/home/vulkan/web-test/index.html`. Python 3 was used to serve the content temporarily on port `8080`, and `curl` confirmed that the HTML page could be retrieved locally.

The web content folder was configured with `0755` permissions, and `index.html` was configured with `0644` permissions. A follow-up Python HTTP server test confirmed that the page still worked after the permission change.

SELinux was reviewed and confirmed to be enabled and enforcing. The temporary web content stored under `/home/vulkan/web-test` used the expected `user_home_t` SELinux context because it is located in the user home directory. This is different from a normal Apache web root context such as `httpd_sys_content_t`, but Apache-specific SELinux testing could not be completed because Apache/httpd is not installed.

firewalld was reviewed and TCP port `8080` was temporarily opened for lab testing. The port was verified with `firewall-cmd --list-ports` and then removed again. The rule was not made permanent.

Local and network testing confirmed that the temporary web page could be reached through localhost, the RHEL server IP address and from the Windows host machine.

Web request logging was reviewed. Since Apache/httpd is not installed, standard Apache logs were not available. Python's built-in HTTP server logged requests directly in the terminal where the server was running.

A troubleshooting reflection document was created under `docs/troubleshooting_reflection.md` to document the main blockers, fallback methods, SELinux observations, firewall testing, logging limitations, production limitations and future remediation steps.


## Skills demonstrated

This project demonstrates:

* Red Hat Enterprise Linux administration
* Linux service management checks
* Apache/httpd package readiness checks
* Package and repository troubleshooting
* RHEL subscription and repository limitation documentation
* Web service readiness review
* Alternative tool verification
* Python-based temporary lab web testing
* Static web content creation
* Local web testing with `curl`
* Listening port verification with `ss`
* Linux file ownership and permissions
* Basic web file permission hardening
* SELinux status and context review
* Firewalld review and HTTP access control
* Temporary firewall rule testing
* Local and network service testing where possible
* Log review and troubleshooting
* Git and GitHub workflow
* Markdown documentation
* Screenshot-based evidence collection

---

## Documentation and evidence

Main documentation files:

| File                              | Purpose                                                |
| --------------------------------- | ------------------------------------------------------ |
| `README.md`                       | Main GitHub project overview                           |
| `logbook.md`                      | Step-by-step project documentation                     |
| `docs/troubleshooting_reflection.md` | Troubleshooting findings, limitations and remediation notes |

Screenshot evidence is stored in:

```text
screenshots/
```

Current screenshot evidence:

| Screenshot                                                 | Purpose                                              |
| ---------------------------------------------------------- | ---------------------------------------------------- |
| `screenshot-01-project-structure-and-git-status.png`       | Initial project structure and Git status             |
| `screenshot-02a-rhel-baseline-system.png`                  | RHEL baseline system information                     |
| `screenshot-02b-rhel-baseline-security-and-resources.png`  | RHEL baseline security and resource checks           |
| `screenshot-03-rhel-httpd-package-check.png`               | Apache/httpd package and repository limitation check |
| `screenshot-04a-rhel-repository-readiness.png`             | Repository and subscription readiness review         |
| `screenshot-04b-rhel-web-service-readiness.png`            | Alternative web service and port readiness review    |
| `screenshot-05a-rhel-temporary-web-content.png`            | Temporary web content creation                       |
| `screenshot-05b-rhel-python-http-server-test.png`          | Python HTTP server and local curl test               |
| `screenshot-06a-rhel-web-file-permissions.png`             | Initial web file permission review                   |
| `screenshot-06b-rhel-web-file-permissions.png`             | Final web file permission verification               |
| `screenshot-06c-rhel-web-permission-service-test.png`      | Web service test after permission changes            |
| `screenshot-07a-rhel-selinux-status.png`                   | SELinux status and enforcing mode verification       |
| `screenshot-07b-rhel-web-content-contexts.png`             | SELinux contexts for temporary web content           |
| `screenshot-08a-rhel-firewalld-before-port-8080.png`       | Firewalld status before opening port 8080            |
| `screenshot-08b-rhel-firewalld-port-8080-added.png`        | Temporary firewalld rule for port 8080 added         |
| `screenshot-08c-rhel-firewalld-port-8080-removed.png`      | Temporary firewalld rule for port 8080 removed       |
| `screenshot-09a-rhel-local-and-ip-web-test.png`            | Localhost and server IP web access test from RHEL    |
| `screenshot-09b-windows-browser-web-test.png`              | Windows host web access test to the RHEL server      |
| `screenshot-09c-rhel-web-test-cleanup.png`                 | Python server and firewall cleanup verification      |
| `screenshot-10a-rhel-python-web-request-logs.png`          | Python HTTP server request log entries               |
| `screenshot-10b-windows-web-request-success.png`           | Windows PowerShell web request returning 200 OK      |
| `screenshot-10c-rhel-log-review-cleanup.png`               | Log review cleanup and final port/firewall check     |
| `screenshot-11a-troubleshooting-reflection-document.png`   | Troubleshooting reflection document evidence         |

----------------------------------------------------- | ---------------------------------------------------- |
| `screenshot-01-project-structure-and-git-status.png`      | Initial project structure and Git status             |
| `screenshot-02a-rhel-baseline-system.png`                 | RHEL baseline system information                     |
| `screenshot-02b-rhel-baseline-security-and-resources.png` | RHEL baseline security and resource checks           |
| `screenshot-03-rhel-httpd-package-check.png`              | Apache/httpd package and repository limitation check |
| `screenshot-04a-rhel-repository-readiness.png`            | Repository and subscription readiness review         |
| `screenshot-04b-rhel-web-service-readiness.png`           | Alternative web service and port readiness review    |
| `screenshot-05a-rhel-temporary-web-content.png`           | Temporary web content creation                       |
| `screenshot-05b-rhel-python-http-server-test.png`         | Python HTTP server and local curl test               |
| `screenshot-06a-rhel-web-file-permissions.png`            | Initial web file permission review                   |
| `screenshot-06b-rhel-web-file-permissions.png`            | Final web file permission verification               |
| `screenshot-06c-rhel-web-permission-service-test.png`     | Web service test after permission changes            |
| `screenshot-07a-rhel-selinux-status.png`                  | SELinux status and enforcing mode verification       |
| `screenshot-07b-rhel-web-content-contexts.png`            | SELinux contexts for temporary web content           |
| `screenshot-08a-rhel-firewalld-before-port-8080.png`      | Firewalld status before opening port 8080            |
| `screenshot-08b-rhel-firewalld-port-8080-added.png`       | Temporary firewalld rule for port 8080 added         |
| `screenshot-08c-rhel-firewalld-port-8080-removed.png`     | Temporary firewalld rule for port 8080 removed       |

---

## Part 7 — SELinux web context review

Status: Complete

This part reviewed SELinux status and SELinux contexts for the temporary web content.

Commands used:

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

Results:

* SELinux was enabled.
* SELinux was running in enforcing mode.
* The loaded policy was `targeted`.
* The temporary web content folder was labeled with `user_home_t`.
* The `index.html` file was labeled with `user_home_t`.
* Folder permissions were confirmed as `0755`.
* File permissions were confirmed as `0644`.
* Owner and group were confirmed as `vulkan:vulkan`.
* No temporary Python HTTP server was listening on port `8080` after the previous test.

Notes:

The `user_home_t` context is expected because the temporary web content is stored under `/home/vulkan/web-test`.

A normal Apache/httpd web root would usually use a different SELinux context, such as `httpd_sys_content_t`. Because Apache/httpd could not be installed, Apache-specific SELinux behavior could not be tested in this lab.

Screenshots:

```text
screenshots/screenshot-07a-rhel-selinux-status.png
screenshots/screenshot-07b-rhel-web-content-contexts.png
```

---

## Part 8 — Firewalld port 8080 test

Status: Complete

This part reviewed the active firewalld configuration and temporarily opened TCP port `8080` for lab testing.

Because Apache/httpd could not be installed on the unregistered RHEL system, the lab continued using Python's built-in HTTP server on port `8080` as a temporary web service test.

Commands used:

```bash
sudo firewall-cmd --state
sudo firewall-cmd --get-active-zones
sudo firewall-cmd --list-all

sudo firewall-cmd --add-port=8080/tcp
sudo firewall-cmd --list-ports

sudo firewall-cmd --remove-port=8080/tcp
sudo firewall-cmd --list-ports
```

Results:

* Firewalld was running.
* The active firewall zone was reviewed.
* TCP port `8080` was temporarily added.
* The open port list showed `8080/tcp` after it was added.
* TCP port `8080` was removed after testing.
* The final port list no longer showed `8080/tcp`.

Notes:

The firewall rule was not made permanent. This was intentional because the purpose was to demonstrate temporary firewall testing for the lab.

A warning appeared when removing port `8080` a second time because the port had already been removed. This confirmed that the first removal had already succeeded.

Screenshots:

```text
screenshots/screenshot-08a-rhel-firewalld-before-port-8080.png
screenshots/screenshot-08b-rhel-firewalld-port-8080-added.png
screenshots/screenshot-08c-rhel-firewalld-port-8080-removed.png
```

---

## Part 9 — Local and network testing

Status: Complete

This part tested access to the temporary Python web server from localhost, the RHEL server IP address and the Windows host machine.

Because Apache/httpd could not be installed, Python's built-in HTTP server continued to be used as a temporary lab web service on port `8080`.

Commands used:

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

Windows host testing used:

```powershell
Invoke-WebRequest http://192.168.80.134:8080 -UseBasicParsing
```

Results:

* Port `8080/tcp` was temporarily opened in firewalld.
* The Python HTTP server was started from `/home/vulkan/web-test`.
* Localhost access from RHEL was tested.
* Server IP access using `192.168.80.134` was tested.
* Windows host access to the temporary web page was tested.
* The temporary Python server was stopped after testing.
* Port `8080/tcp` was removed from firewalld after testing.

Screenshots:

```text
screenshots/screenshot-09a-rhel-local-and-ip-web-test.png
screenshots/screenshot-09b-windows-browser-web-test.png
screenshots/screenshot-09c-rhel-web-test-cleanup.png
```

---

## Part 10 — Web server log review

Status: Complete

This part reviewed request logging behavior for the temporary Python web server and confirmed that Apache/httpd logs were unavailable because Apache/httpd was not installed.

Python's built-in HTTP server logs web requests directly in the terminal where the server is running. This differs from Apache/httpd, which normally writes access and error logs under `/var/log/httpd/`.

Commands used:

```bash
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

Results:

* Python HTTP server request logs were visible in the terminal.
* Successful requests returned HTTP `200 OK`.
* Windows PowerShell confirmed successful network access to the temporary web page.
* Apache/httpd log review could not be performed because Apache/httpd was not installed.
* System logs were searched with `journalctl`.
* The temporary server and firewall opening were cleaned up after testing.

Screenshots:

```text
screenshots/screenshot-10a-rhel-python-web-request-logs.png
screenshots/screenshot-10b-windows-web-request-success.png
screenshots/screenshot-10c-rhel-log-review-cleanup.png
```

---

## Part 11 — Troubleshooting reflection

Status: Complete

This part created a troubleshooting reflection document that summarizes the main issues, limitations, fallback methods and remediation steps from the lab.

Created file:

```text
docs/troubleshooting_reflection.md
```

The reflection document covers:

* Apache/httpd being unavailable.
* RHEL subscription and repository limitations.
* The unavailable `nano` editor.
* The heredoc fallback using `cat`.
* Python's built-in HTTP server as a temporary lab fallback.
* File permission findings.
* SELinux context findings.
* firewalld port `8080` testing.
* Local, network and Windows host testing.
* Python request logging.
* Production limitations.
* Future remediation steps for a proper Apache/httpd setup.

Screenshot:

```text
screenshots/screenshot-11a-troubleshooting-reflection-document.png
```

---

## Notes

This is a lab environment and not a production system.

The project is created for learning, documentation and portfolio demonstration.

The RHEL system is currently not registered with Red Hat subscription management and has no enabled repositories. Because of this, Apache/httpd could not be installed through `dnf`.

This limitation is documented throughout the lab instead of ignored. Future remediation would require registering the RHEL system or enabling a valid package repository before installing Apache/httpd.

Python 3 is available on the system and was used for temporary local web testing in the lab. Python’s built-in HTTP server is not a production replacement for Apache/httpd.

The temporary web content was stored under `/home/vulkan/web-test` and configured with basic readable permissions for lab testing.

SELinux remained enabled and enforcing during the lab. The temporary web content used the `user_home_t` context because it was stored in the user's home directory.

Firewalld was used to temporarily open and remove TCP port `8080` during testing. The port opening was not made permanent.

Local and network testing confirmed that the temporary web content could be reached from the RHEL server itself and from the Windows host machine by using the RHEL server IP address.

Python's built-in HTTP server logged requests directly in the terminal. Standard Apache/httpd access and error logs were not available because Apache/httpd was not installed.

The troubleshooting reflection document in `docs/troubleshooting_reflection.md` summarizes the main issues, workarounds, production limitations and future remediation steps.
