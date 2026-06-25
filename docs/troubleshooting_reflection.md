# Troubleshooting Reflection

## Project context

This document summarizes the main troubleshooting findings from the RHEL Web Server Operations Lab.

The original goal of the lab was to configure and document a basic Apache/httpd-based web server on Red Hat Enterprise Linux. During the lab, Apache/httpd could not be installed because the RHEL system was not registered with Red Hat subscription management and had no enabled repositories.

Because of this limitation, the lab was adapted into a realistic web service readiness and troubleshooting project. Instead of pretending that Apache/httpd was available, the limitation was documented and a temporary Python-based HTTP server was used for static web testing.

Public documentation identity used in this project: Vulkan.

---

## Main issue: Apache/httpd was unavailable

The first major issue was that Apache/httpd was not installed on the RHEL server.

The following checks confirmed this:

```bash
rpm -q httpd
which httpd
systemctl status httpd --no-pager
```

The results showed that the `httpd` package was not installed, the `httpd` command was not found, and the `httpd.service` unit was not available.

This meant that normal Apache service configuration could not be completed on the current system.

---

## Repository and subscription limitation

The next troubleshooting step was to check whether Apache/httpd could be installed.

The following commands were used:

```bash
sudo dnf info httpd
sudo dnf repolist
sudo dnf install -y httpd
sudo subscription-manager status
sudo dnf repolist --all
```

The results showed that the RHEL system was not registered with an entitlement server and had no enabled repositories.

This was the root cause of the Apache/httpd installation failure.

In a real environment, this would need to be resolved before installing or maintaining packages through DNF.

Possible remediation would include:

* Registering the system with Red Hat subscription management.
* Attaching a valid subscription.
* Enabling the required RHEL repositories.
* Using an approved internal repository or mirror.
* Re-running the package installation after repository access is restored.

---

## Alternative tool review

Because Apache/httpd was unavailable, alternative web service tools were checked.

The following commands were used:

```bash
rpm -q nginx
rpm -q lighttpd
rpm -q python3
which python3
```

Nginx and Lighttpd were not installed.

Python 3 was installed and available at:

```text
/usr/bin/python3
```

This made it possible to continue the lab with Python's built-in HTTP server as a temporary test method.

This was not treated as a production replacement for Apache/httpd. It was used only to verify basic static web content, file permissions, local access, network access and request logging.

---

## Text editor limitation

During web content creation, the `nano` editor was not available.

Because package installation was blocked by the repository limitation, installing nano was not possible through DNF.

Instead, the `index.html` file was created using a heredoc with `cat`.

This demonstrated a useful fallback method for creating files on a minimal Linux system.

Example:

```bash
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
```

---

## Temporary Python HTTP server fallback

The temporary web content was created under:

```text
/home/vulkan/web-test
```

The Python web server was started with:

```bash
python3 -m http.server 8080
```

The server successfully served the static HTML page on port `8080`.

Local testing confirmed that the page could be retrieved from:

```text
http://127.0.0.1:8080
```

Network testing confirmed that the page could also be reached using the server IP:

```text
http://192.168.80.134:8080
```

Windows testing confirmed that the host machine could reach the temporary web page through the RHEL server IP after the firewall was configured to allow port `8080`.

---

## File permission findings

The temporary web folder and HTML file were reviewed with:

```bash
ls -ld ~/web-test
ls -l ~/web-test/index.html
stat ~/web-test
stat ~/web-test/index.html
```

The folder was configured with:

```text
0755 / drwxr-xr-x
```

The HTML file was configured with:

```text
0644 / -rw-r--r--
```

These permissions allow the owner to manage the files while allowing the content to be read for basic web testing.

The final ownership was:

```text
vulkan:vulkan
```

This was appropriate for the lab environment.

---

## SELinux findings

SELinux was checked with:

```bash
getenforce
sestatus
```

The system was running in enforcing mode with the targeted policy.

The temporary web content was checked with:

```bash
ls -Z
ls -Zd ~/web-test
ls -Z ~/web-test/index.html
stat ~/web-test
stat ~/web-test/index.html
```

The folder and file were labeled with:

```text
unconfined_u:object_r:user_home_t:s0
```

This is expected because the files were stored inside the user's home directory.

A normal Apache web root would usually use a different context, such as:

```text
httpd_sys_content_t
```

Because Apache/httpd was not installed, Apache-specific SELinux behavior could not be tested.

No SELinux policy or context changes were made during this part of the lab.

---

## Firewalld findings

firewalld was reviewed with:

```bash
sudo firewall-cmd --state
sudo firewall-cmd --get-active-zones
sudo firewall-cmd --list-all
```

Port `8080/tcp` was temporarily opened for testing:

```bash
sudo firewall-cmd --add-port=8080/tcp
sudo firewall-cmd --list-ports
```

After testing, port `8080/tcp` was removed:

```bash
sudo firewall-cmd --remove-port=8080/tcp
sudo firewall-cmd --list-ports
```

The firewall rule was not made permanent. This was intentional because the Python HTTP server was only used temporarily for lab testing.

The firewall test demonstrated how access to a temporary web service can be controlled with firewalld.

---

## Local and network testing findings

Local and network access were tested after temporarily allowing port `8080/tcp` through firewalld.

The Python HTTP server was started from the temporary web content folder:

```bash
cd ~/web-test
python3 -m http.server 8080
```

Local access from the RHEL server was tested with:

```bash
curl http://127.0.0.1:8080
```

Network access using the RHEL server IP was tested with:

```bash
curl http://192.168.80.134:8080
```

Windows access was tested from the host machine using:

```powershell
Invoke-WebRequest http://192.168.80.134:8080 -UseBasicParsing
```

The Windows request returned status code `200 OK`, confirming that the host machine could reach the temporary Python web server over the network.

This demonstrated the difference between localhost testing, server IP testing and external host testing.

---

## Web request log findings

Because Apache/httpd was not installed, standard Apache log files were not available.

The Apache log directory was checked with:

```bash
ls -l /var/log/httpd 2>/dev/null || echo "Apache/httpd log directory not available"
rpm -q httpd
```

The result confirmed that Apache/httpd log review could not be performed because Apache/httpd was not installed.

Python's built-in HTTP server logged requests directly in the terminal where the server was running.

Example request log pattern:

```text
"GET / HTTP/1.1" 200 -
```

This showed that the temporary server received and served web requests successfully.

System logs were also searched with:

```bash
journalctl --since "today" --no-pager | grep -i python || true
journalctl --since "today" --no-pager | grep -i http || true
journalctl --since "today" --no-pager | grep -i firewall || true
```

This helped demonstrate the difference between application-specific request logs and general system journal review.

---

## Cleanup findings

After testing, the temporary Python HTTP server was stopped with `Ctrl+C`.

Port `8080` was checked again with:

```bash
ss -tulpen | grep ':8080' || true
```

The final check showed that nothing was listening on port `8080`.

The temporary firewalld rule was removed with:

```bash
sudo firewall-cmd --remove-port=8080/tcp
sudo firewall-cmd --list-ports
```

The final firewall check confirmed that `8080/tcp` was no longer listed.

This returned the system to a cleaner post-test state.

---

## Production limitations

This lab was performed in a constrained environment.

The current setup is not production-ready because:

* Apache/httpd is not installed.
* The RHEL system is not registered.
* No enabled package repositories are available.
* Python's built-in HTTP server is not a production web server.
* The temporary web content is stored under a user home directory.
* The SELinux context is `user_home_t`, not a standard Apache web content context.
* The firewall opening for port `8080` was temporary.
* No permanent web service unit was configured.
* No TLS/HTTPS configuration was completed.
* No production logging or monitoring was configured.

These limitations were intentionally documented instead of hidden.

---

## Future remediation

To turn this into a normal Apache/httpd web server setup, the following actions would be needed:

1. Register the RHEL system with Red Hat subscription management.
2. Enable the required RHEL repositories.
3. Install Apache/httpd with DNF.
4. Place web content under a standard web root such as `/var/www/html`.
5. Confirm or restore the correct SELinux context for Apache content.
6. Start and enable the `httpd` service.
7. Allow HTTP and HTTPS services through firewalld.
8. Test access locally and over the network.
9. Review Apache access and error logs.
10. Document final service state and operational checks.

---

## Lessons learned

This lab demonstrated that system administration work often depends on verifying the environment before configuring services.

The most important finding was that Apache/httpd could not be installed because repository and subscription access were not available. Instead of ignoring this blocker, the lab documented the limitation and continued with realistic fallback testing.

So that was a small failure from my side.

The project also showed how to verify a system baseline, check package availability, troubleshoot repository access, create temporary web content, test local and network web access, review permissions, inspect SELinux contexts, manage firewalld rules and review available logs.

The final result is not a production Apache server, but it is a useful and honest sysadmin operations lab that demonstrates troubleshooting, documentation and operational verification skills.
