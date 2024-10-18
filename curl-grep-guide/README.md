# 🛠️ Curl & Grep Command Guide

Welcome to this guide on using `curl` and `grep`! In this README, we'll walk through what these commands do, how to use them, and explore their different options in various scenarios. Let's get started! 🚀

---

## 🔗 cURL (Client URL) Command

`curl` is a powerful command-line tool used for transferring data to and from servers. It supports various protocols such as HTTP, HTTPS, FTP, and more. It is widely used for interacting with web APIs, downloading files, or even making requests to websites.

### 📖 What can you do with `curl`?
- **Download files** from the web.
- **Send data** to a server (e.g., for API testing).
- **Access APIs** with GET, POST, PUT, DELETE requests.
- **Upload files** to a remote server.
- **Follow redirects** and manage cookies automatically.

### 📋 cURL Options Table

| **Option**           | **Description**                                                                                          | **Example**                                    |
|----------------------|----------------------------------------------------------------------------------------------------------|------------------------------------------------|
| `-X, --request`       | Specify a custom request method like GET, POST, PUT, DELETE.                                              | `curl -X POST https://example.com/api`         |
| `-d, --data`          | Send POST data with a request.                                                                            | `curl -d "name=John" https://example.com`      |
| `-H, --header`        | Pass custom headers to the server.                                                                        | `curl -H "Authorization: Bearer TOKEN"`        |
| `-o, --output`        | Save the output to a file.                                                                                | `curl -o file.txt https://example.com`         |
| `-L, --location`      | Follow redirects.                                                                                         | `curl -L https://example.com`                  |
| `-b, --cookie`        | Send cookies with the request.                                                                            | `curl -b "session=abc" https://example.com`    |
| `-u, --user`          | User authentication for accessing resources.                                                              | `curl -u user:pass https://example.com`        |
| `--http2`             | Use HTTP/2 protocol for the request.                                                                      | `curl --http2 https://example.com`             |
| `-I, --head`          | Fetch only the headers of a resource.                                                                     | `curl -I https://example.com`                  |
| `-v, --verbose`       | Enable detailed output for debugging.                                                                     | `curl -v https://example.com`                  |
| `--compressed`        | Request compressed content from the server.                                                               | `curl --compressed https://example.com`        |
| `-F, --form`          | Submit multipart form data (for file uploads).                                                            | `curl -F "file=@/path/to/file" https://...`    |

### 📝 Examples

- **Basic GET request**:
  ```bash
  curl https://jsonplaceholder.typicode.com/posts/1
  ```
  This fetches the data for post ID 1 from a mock JSON API.

- **Download a file**:
  ```bash
  curl -O https://example.com/file.zip
  ```
  This downloads the file and saves it with the remote name.

- **POST data to an API**:
  ```bash
  curl -X POST -d "name=John&age=30" https://api.example.com/create
  ```
  This sends a POST request with form data to an API.

- **Send custom headers**:
  ```bash
  curl -H "Authorization: Bearer my-token" https://api.example.com/data
  ```
  This sends a request with an authentication token in the header.

---

## 🔍 Grep Command

`grep` is a powerful command-line utility used for searching text within files or command outputs. It supports regular expressions and is highly useful for filtering results based on patterns.

### 📖 What can you do with `grep`?
- **Search for text patterns** within files or outputs.
- **Filter logs** for specific keywords.
- **Highlight specific patterns** within files.
- **Combine it with other commands** like `ls`, `cat`, or `curl` to refine results.

### 📋 Grep Options Table

| **Option**           | **Description**                                                                                          | **Example**                                    |
|----------------------|----------------------------------------------------------------------------------------------------------|------------------------------------------------|
| `-i, --ignore-case`   | Perform case-insensitive matching.                                                                        | `grep -i "error" file.txt`                     |
| `-r, --recursive`     | Search recursively through directories.                                                                   | `grep -r "TODO" /path/to/project`              |
| `-v, --invert-match`  | Invert match to show lines that don't contain the pattern.                                                | `grep -v "DEBUG" log.txt`                      |
| `-c, --count`         | Display the count of matching lines.                                                                      | `grep -c "error" log.txt`                      |
| `-n, --line-number`   | Show line numbers with matching lines.                                                                    | `grep -n "main" file.c`                        |
| `-o, --only-matching` | Print only the matched parts of a line.                                                                   | `grep -o "https://[a-z]*" file.txt`            |
| `-l, --files-with-matches` | List files containing matches.                                                                      | `grep -l "TODO" *.txt`                         |
| `--color`             | Highlight matches in the output.                                                                          | `grep --color "error" log.txt`                 |

### 📝 Examples

- **Search for a word in a file**:
  ```bash
  grep "hello" file.txt
  ```
  This finds all lines containing the word "hello" in `file.txt`.

- **Case-insensitive search**:
  ```bash
  grep -i "error" log.txt
  ```
  This searches for the word "error" in a case-insensitive manner.

- **Recursive search in a directory**:
  ```bash
  grep -r "TODO" /path/to/project
  ```
  This searches for the keyword "TODO" in all files within a project directory.

- **Find lines without a keyword**:
  ```bash
  grep -v "DEBUG" log.txt
  ```
  This finds all lines in `log.txt` that do NOT contain the word "DEBUG".

- **Show only matching parts of a line**:
  ```bash
  grep -o "https://[a-z]*" file.txt
  ```
  This extracts all URLs starting with `https://` from a text file.

---

## ⚙️ Combining cURL & Grep

`curl` and `grep` can be used together to retrieve data and filter the output. Here's an example:

### Example: Fetching and Searching API Data

```bash
curl https://jsonplaceholder.typicode.com/posts | grep "userId"
```

This command fetches a list of posts and then filters only the lines that contain `userId`.

Another useful case is to download web content and search for specific patterns:

### Example: Download a webpage and search for a keyword

```bash
curl https://example.com -s | grep -i "privacy"
```

This command silently fetches the contents of a webpage and searches for the word "privacy" (case-insensitive).

---

## 📚 Conclusion

`curl` and `grep` are extremely powerful and flexible tools. Whether you're downloading files, making API requests, or searching through logs and files, these commands have you covered! 🚀

Explore more possibilities by combining them with other commands to build complex data pipelines. Happy hacking! 😎
