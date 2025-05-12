# HYDRA Commands Cheatsheet

Welcome to the HYDRA Commands Cheatsheet! This document provides a quick reference and easy navigation for common HYDRA commands. Use the table of contents below to jump straight to the section you need.

---

## Table of Contents

- [Basic Usage](#basic-usage)
- [Authentication Attacks](#authentication-attacks)
- [Supported Protocols & Services](#supported-protocols--services)
- [Common Examples](#common-examples)
- [Brute Forcing with Wordlists](#brute-forcing-with-wordlists)
- [Advanced Options](#advanced-options)
- [Tips & Best Practices](#tips--best-practices)
- [References](#references)

---

## Basic Usage

```bash
hydra [OPTIONS] [TARGET] [MODULE]
```

- `-L` : Path to a file containing a list of usernames
- `-l` : Single username
- `-P` : Path to a file containing a list of passwords
- `-p` : Single password
- `-t` : Number of parallel tasks (threads)
- `-s` : Port number
- `-vV` : Verbose mode (shows attempts)
- `-o` : Output file for results

---

## Authentication Attacks

- **SSH:**
  ```bash
  hydra -l root -P passwords.txt ssh://192.168.1.10
  ```
- **FTP:**
  ```bash
  hydra -L users.txt -P pass.txt ftp://example.com
  ```
- **HTTP-POST-FORM:**
  ```bash
  hydra -L users.txt -P passwords.txt example.com http-post-form "/login.php:user=^USER^&pass=^PASS^:F=incorrect"
  ```

---

## Supported Protocols & Services

HYDRA supports numerous protocols. Common examples:

- ftp
- ssh
- telnet
- http-get
- http-post-form
- smb
- rdp
- vnc
- smtp
- pop3
- imap

See all supported modules:

```bash
hydra -U
```

---

## Common Examples

- **Brute force SSH with default port:**
  ```bash
  hydra -L users.txt -P passwords.txt ssh://target
  ```
- **Brute force FTP with custom port:**
  ```bash
  hydra -l admin -P passwords.txt ftp://target -s 2121
  ```
- **Brute force HTTP Basic Auth:**
  ```bash
  hydra -L users.txt -P passwords.txt -s 8080 http-get://target/protected
  ```

---

## Brute Forcing with Wordlists

- **Set username and password lists:**
  ```bash
  hydra -L usernames.txt -P passwords.txt [service]://[target]
  ```
- **Try all combinations (usernames * passwords):**
  ```bash
  hydra -C combos.txt [service]://[target]   # combos.txt contains user:pass pairs
  ```

---

## Advanced Options

- `-f` : Exit when a valid credential is found
- `-V` : Print each attempt
- `-e nsr` : Try blank/null password (n), username as password (s), reversed login (r)
- `-x min:max:charset` : Generate passwords on the fly (e.g. -x 4:6:a1 for 4-6 length, alpha+num)
- `-w` : Timeout for each connect attempt

---

## Tips & Best Practices

- Always get permission before running HYDRA on any network or system you do not own.
- Use verbose mode for debugging (`-vV`).
- Customise thread count (`-t`) based on target and network speed.
- Check for account lockouts before running brute force attacks.
- Save results using `-o results.txt`.

---

## References

- [HYDRA GitHub](https://github.com/vanhauser-thc/thc-hydra)
- [Official Documentation](https://github.com/vanhauser-thc/thc-hydra/wiki)
- [Kali Tools HYDRA](https://www.kali.org/tools/hydra/)

---

> **Disclaimer:** Use HYDRA responsibly and only on systems you are authorized to test.
