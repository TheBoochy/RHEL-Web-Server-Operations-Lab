# RHEL Web Server Operations Lab

## Overview

RHEL Web Server Operations Lab is a voluntary sysadmin portfolio project focused on basic Red Hat Enterprise Linux web server administration and web service readiness checks.

The lab is designed to practice service management, package checks, repository troubleshooting, service readiness review, file permissions, SELinux review, firewalld configuration, log review and documentation.

Public documentation uses the name **Vulkan**.

---

## Scenario

A small organization needs a basic internal web server hosted on Red Hat Enterprise Linux.

The goal of this lab is to configure, verify and document a simple RHEL-based web service environment using a structured sysadmin workflow.

During the lab, the Apache/httpd package was checked and confirmed to be unavailable on the current system because the RHEL server is not registered and has no enabled repositories. This limitation is documented as part of the troubleshooting process.

The lab continues by reviewing web service readiness, repository state, available alternatives and security controls.

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
| Part 5  | Temporary web content and Python HTTP server test      | Planned  |
| Part 6  | Web file permissions                                   | Planned  |
| Part 7  | SELinux web context review                             | Planned  |
| Part 8  | Firewalld HTTP access                                  | Planned  |
| Part 9  | Local and network testing                              | Planned  |
| Part 10 | Web server log review                                  | Planned  |
| Part 11 | Troubleshooting reflection                             | Planned  |
| Part 12 | Final README and GitHub polish                         | Planned  |

---

## Project structure

```text
RHEL-Web-Server-Operations-Lab/
├── docs/
│   └── .gitkeep
├── results/
│   └── .gitkeep
├── screenshots/
│   ├── .gitkeep
│   ├── screenshot-01-project-structure-and-git-status.png
│   ├── screenshot-02a-rhel-baseline-system.png
│   ├── screenshot-02b-rhel-baseline-security-and-resources.png
│   ├── screenshot-03-rhel-httpd-package-check.png
│   ├── screenshot-04a-rhel-repository-readiness.png
│   └── screenshot-04b-rhel-web-service-readiness.png
├── scripts/
│   └── .gitkeep
├── logbook.md
└── README.md
```

---

## Current progress

The project currently has the initial repository structure completed, the RHEL server baseline verified, the web server package check completed and the web service readiness limitation reviewed.

The baseline verification confirms the server identity, operating system, network configuration, disk usage, memory usage, SELinux mode and firewalld status before any web server package checks or configuration changes are made.

The web server package check confirmed that Apache/httpd is not installed. The `httpd` command and `httpd.service` were not found. Package lookup and installation attempts failed because the RHEL system is not registered with an entitlement server and has no enabled repositories.

The repository readiness review confirmed that a `redhat.repo` file exists, but the system is not registered and DNF reports no usable repositories. The web service readiness check confirmed that Nginx and Lighttpd are not installed, while Python 3 is available. No services were listening on common web ports `80`, `443` or `8080`.

This means the lab will continue using temporary Python-based web testing where appropriate, while clearly documenting that Apache/httpd could not be installed in the current RHEL environment.

---

## Skills demonstrated

This project will demonstrate:

* Red Hat Enterprise Linux administration
* Linux service management checks
* Apache/httpd package readiness checks
* Package and repository troubleshooting
* RHEL subscription and repository limitation documentation
* Web service readiness review
* Alternative tool verification
* Python-based temporary lab web testing
* Linux file ownership and permissions
* SELinux status and context review
* Firewalld review and HTTP access control
* Local and network service testing where possible
* Log review and troubleshooting
* Git and GitHub workflow
* Markdown documentation
* Screenshot-based evidence collection

---

## Documentation and evidence

Main documentation files:

| File         | Purpose                            |
| ------------ | ---------------------------------- |
| `README.md`  | Main GitHub project overview       |
| `logbook.md` | Step-by-step project documentation |

Screenshot evidence is stored in:

```text
screenshots/
```

Current screenshot evidence:

| Screenshot                                                | Purpose                                              |
| --------------------------------------------------------- | ---------------------------------------------------- |
| `screenshot-01-project-structure-and-git-status.png`      | Initial project structure and Git status             |
| `screenshot-02a-rhel-baseline-system.png`                 | RHEL baseline system information                     |
| `screenshot-02b-rhel-baseline-security-and-resources.png` | RHEL baseline security and resource checks           |
| `screenshot-03-rhel-httpd-package-check.png`              | Apache/httpd package and repository limitation check |
| `screenshot-04a-rhel-repository-readiness.png`            | Repository and subscription readiness review         |
| `screenshot-04b-rhel-web-service-readiness.png`           | Alternative web service and port readiness review    |

---

## Notes

This is a lab environment and not a production system.

The project is created for learning, documentation and portfolio demonstration.

The RHEL system is currently not registered with Red Hat subscription management and has no enabled repositories. Because of this, Apache/httpd could not be installed through `dnf`.

This limitation will be documented throughout the lab instead of ignored. Future remediation would require registering the RHEL system or enabling a valid package repository before installing Apache/httpd.

Python 3 is available on the system and may be used later for temporary local web testing in the lab. Python’s built-in HTTP server is not a production replacement for Apache/httpd.
