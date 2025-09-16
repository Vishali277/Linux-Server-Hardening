# Linux Server Hardening

> **Project Execution Note:** Due to persistent technical failures with multiple virtual machine installations (both Ubuntu and Kali Linux) under a strict deadline, this submission is documentation-based. The following report details the exact steps, commands, and expected outcomes of the server hardening process, demonstrating a complete understanding of the required concepts and procedures.

---

## 🚀 Hardening Process and Commands

The hardening process follows a structured approach to layering security controls. A full list of commands used can be found in `commands.txt`.

1.  **Initial User Setup**: A new non-root user (`testuser`) is created and given `sudo` privileges to avoid operating as `root`.
2.  **Firewall Configuration**: The UFW firewall is enabled and configured to allow only `OpenSSH` traffic, blocking all other unused ports.
3.  **SSH Securitization**: SSH access is hardened by deploying SSH keys and then disabling both direct `root` login and password-based authentication in the `sshd_config` file.
4.  **Intrusion Prevention**: `Fail2Ban` is installed and enabled to automatically monitor SSH logs and ban IP addresses that exhibit brute-force attack patterns.

---

## 📝 Analysis of Security Posture: Before vs. After

### **Before Hardening (Expected State)**

* **Firewall:** `INACTIVE`. All network ports would be open.
* **Access Control:** Direct `root` login via SSH would be permitted.
* **Authentication:** Password-based authentication would be enabled, making the server vulnerable to brute-force attacks.
* **Threat Mitigation:** No automated threat mitigation would be in place.

### **After Hardening (Expected State)**

* **Firewall:** `ACTIVE`. Only the necessary SSH port (22) would be open.
* **Access Control:** `root` login would be disabled.
* **Authentication:** Secure SSH key-based authentication would be enforced.
* **Threat Mitigation:** `Fail2Ban` would be actively monitoring and blocking malicious IPs.

---

## 🧪 Testing and Validation

The effectiveness of the hardening steps would be validated as follows:

1.  **SSH Validation**: An attempt to `ssh root@SERVER_IP` would be refused. An attempt to log in as `testuser` using a password would also be refused. A successful login would only be possible for `testuser` using the SSH key.
2.  **Fail2Ban Validation**: The command `sudo fail2ban-client status sshd` would confirm the service is active and monitoring SSH logs.

---

## 📁 Files in Repository

* `README.md`: This detailed report of the hardening process and expected outcomes.
* `summary.txt`: A text summary of the server's before and after security posture.
* `commands.txt`: A complete list of the shell commands that would be used.
* **(Note: Screenshots were omitted due to the inability to complete the live installation.)**
