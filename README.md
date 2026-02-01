````md
# 📱➡️💻 SSH Into Your Phone (Termux) From Your PC — Quick Guide

This guide shows how to SSH into your **Android phone running Termux** from a **PC** on the same Wi-Fi.

---

## ✅ Requirements
- Phone: **Termux installed**
- PC: **SSH client**
  - Linux/macOS: built-in `ssh`
  - Windows: PowerShell / CMD / Git Bash

---

# 1) 📲 Setup SSH Server on Phone (Termux)

## Install OpenSSH
```bash
pkg update
pkg install openssh
````

## Start the SSH server

```bash
sshd
```

> Termux SSH usually runs on port **8022** (NOT 22).

---

# 2) 🔐 Set a Password (Important)

You need a password for login (unless using SSH keys).

```bash
passwd
```

Type your password (it won’t show on screen, that’s normal).

---

# 3) 👤 Find Your Termux Username

```bash
whoami
```

Example output:

```
u0_a443
```

---

# 4) 🌐 Find Your Phone IP Address

```bash
ip a
```

Look for something like:

```
192.168.1.13
```

---

# 5) 💻 SSH From PC → Phone

Use this command on your PC:

```bash
ssh -p 8022 u0_a443@192.168.1.13
```

### Example

```bash
ssh -p 8022 u0_a443@192.168.1.13
```

Then enter the password you set in Termux.

---

# 6) ✅ Confirm SSH Is Listening (If Connection Fails)

On your phone (Termux), check port 8022:

```bash
ss -tulnp | grep 8022
```

If you see `LISTEN` → SSH is running.

If nothing shows → start it again:

```bash
pkill sshd
sshd
```

---

# 7) ❌ Fix: "Permission denied"

This usually means:

* wrong password
* wrong username
* your PC is trying key-login only

### Force password login:

```bash
ssh -o PreferredAuthentications=password -o PubkeyAuthentication=no -p 8022 u0_a443@192.168.1.13
```

---

# 8) 🔥 Optional: SSH Login Without Password (SSH Key)

## On your PC: create SSH key

```bash
ssh-keygen
```

## Copy key to phone

```bash
ssh-copy-id -p 8022 u0_a443@192.168.1.13
```

Now login normally:

```bash
ssh -p 8022 u0_a443@192.168.1.13
```

---

# ✅ Quick Checklist

* [ ] `pkg install openssh`
* [ ] `sshd`
* [ ] `passwd`
* [ ] `whoami`
* [ ] `ip a`
* [ ] PC command: `ssh -p 8022 USER@PHONE_IP`

---

```
```
