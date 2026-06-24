# RHEL Web Server Operations Lab

## Overview

RHEL Web Server Operations Lab is a voluntary sysadmin portfolio project focused on basic Red Hat Enterprise Linux web server administration and web service readiness checks.

The lab is designed to practice service management, package checks, repository troubleshooting, file permissions, SELinux review, firewalld configuration, log review and documentation.

Public documentation uses the name **Vulkan**.

---

## Scenario

A small organization needs a basic internal web server hosted on Red Hat Enterprise Linux.

The goal of this lab is to configure, verify and document a simple RHEL-based web service environment using a structured sysadmin workflow.

During the lab, the Apache/httpd package was checked and confirmed to be unavailable on the current system because the RHEL server is not registered and has no enabled repositories. This limitation is documented as part of the troubleshooting process.

The lab focuses on practical administration tasks, verification commands, screenshots and Git-based documentation.

---

## Lab goals

The goals of this lab are to:

* Create a clean Red Hat-focused web server project.
* Verify the RHEL server baseline.
* Check whether Apache/httpd is installed or available.
* Review package and repository readiness.
* Document missing package and repository limitations.
* Review SELinux status and file contexts.
* Review and test firewalld access where possible.
* Test local and network readiness where possible.
* Review service and system logs.
* Document each part with screenshots and Git commits.

---

## Planned parts

| Part    | Topic                                            | Status   |
| ------- | ------------------------------------------------ | -------- |
| Part 1  | Repository setup and planning                    | Complete |
| Part 2  | RHEL server baseline verification                | Complete |
| Part 3  | Web server package check                         | Complete |
| Part 4  | Apache/httpd service setup or service limitation | Planned  |
| Part 5  | Web content deployment or documentation fallback | Planned  |
| Part 6  | Web file permissions                             | Planned  |
| Part 7  | SELinux web context review                       | Planned  |
| Part 8  | Firewalld HTTP access                            | Planned  |
| Part 9  | Local and network testing                        | Planned  |
| Part 10 | Web server log review                            | Planned  |
| Part 11 | Troubleshooting reflection                       | Planned  |
| Part 12 | Final README and GitHub polish                   | Planned  |

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
│   └── screenshot-03-rhel-httpd-package-check.png
├── scripts/
│   └── .gitkeep
├── logbook.md
└── README.md
```

---

## Current progress

The project currently has the initial repository structure completed, the RHEL server baseline verified and the web server package check completed.

The baseline verification confirms the server identity, operating system, network configuration, disk usage, memory usage, SELinux mode and firewalld status before any web server package checks or configuration changes are made.

The web server package check confirmed that Apache/httpd is not installed. The `httpd` command and `httpd.service` were not found. Package lookup and installation attempts failed because the RHEL system is not registered with an entitlement server and has no enabled repositories.

This means the lab will continue by documenting web service readiness, repository limitations and available security controls instead of pretending Apache was installed by divine intervention. Sadly, the Omnissiah does not ship RPMs.

---

## Skills demonstrated

This project will demonstrate:

* Red Hat Enterprise Linux administration
* Linux service management checks
* Apache/httpd package readiness checks
* Package and repository troubleshooting
* RHEL subscription and repository limitation documentation
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

---

## Notes

This is a lab environment and not a production system.

The project is created for learning, documentation and portfolio demonstration.

The RHEL system is currently not registered with Red Hat subscription management and has no enabled repositories. Because of this, Apache/httpd could not be installed through `dnf`.

This limitation will be documented throughout the lab instead of ignored. Future remediation would require registering the RHEL system or enabling a valid package repository before installing Apache/httpd.
