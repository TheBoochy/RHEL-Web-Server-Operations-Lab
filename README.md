# RHEL Web Server Operations Lab

## Overview

RHEL Web Server Operations Lab is a voluntary sysadmin portfolio project focused on basic Red Hat Enterprise Linux web server administration.

The lab is designed to practice service management, package checks, web content deployment, file permissions, SELinux review, firewalld configuration, log review and troubleshooting.

Public documentation uses the name **Vulkan**.

---

## Scenario

A small organization needs a basic internal web server hosted on Red Hat Enterprise Linux.

The goal of this lab is to configure, verify and document a simple RHEL-based web service environment using a structured sysadmin workflow.

The lab focuses on practical administration tasks, verification commands, screenshots and Git-based documentation.

---

## Lab goals

The goals of this lab are to:

* Create a clean Red Hat-focused web server project.
* Verify the RHEL server baseline.
* Check whether Apache/httpd is installed or available.
* Configure and review the web service.
* Create basic internal web content.
* Review file ownership and permissions.
* Review SELinux status and web file contexts.
* Review and test firewalld web access.
* Test local and network web access.
* Review service and web logs.
* Document each part with screenshots and Git commits.

---

## Planned parts

| Part    | Topic                             | Status   |
| ------- | --------------------------------- | -------- |
| Part 1  | Repository setup and planning     | Complete |
| Part 2  | RHEL server baseline verification | Complete |
| Part 3  | Web server package check          | Planned  |
| Part 4  | Apache/httpd service setup        | Planned  |
| Part 5  | Web content deployment            | Planned  |
| Part 6  | Web file permissions              | Planned  |
| Part 7  | SELinux web context review        | Planned  |
| Part 8  | Firewalld HTTP access             | Planned  |
| Part 9  | Local and network testing         | Planned  |
| Part 10 | Web server log review             | Planned  |
| Part 11 | Troubleshooting reflection        | Planned  |
| Part 12 | Final README and GitHub polish    | Planned  |

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
│   └── screenshot-02b-rhel-baseline-security-and-resources.png
├── scripts/
│   └── .gitkeep
├── logbook.md
└── README.md
```

---

## Current progress

The project currently has the initial repository structure completed and the RHEL server baseline verified.

The baseline verification confirms the server identity, operating system, network configuration, disk usage, memory usage, SELinux mode and firewalld status before any web server package checks or configuration changes are made.

---

## Skills demonstrated

This project will demonstrate:

* Red Hat Enterprise Linux administration
* Linux service management
* Apache/httpd web server basics
* Package and repository checking
* Web content deployment
* Linux file ownership and permissions
* SELinux status and context review
* Firewalld review and HTTP access control
* Local and network service testing
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

---

## Notes

This is a lab environment and not a production system.

The project is created for learning, documentation and portfolio demonstration.

If packages cannot be installed because the RHEL system is not registered or has no enabled repositories, that limitation will be documented as part of the troubleshooting process.
