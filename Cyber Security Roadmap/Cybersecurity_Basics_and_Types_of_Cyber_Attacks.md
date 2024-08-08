# Cybersecurity: Basic Concepts and Types of Cyber Attacks

## 1. Basic Concepts of Cybersecurity

**Cybersecurity** refers to the practice of protecting systems, networks, and data from digital attacks, unauthorized access, damage, or theft. The primary goal of cybersecurity is to ensure the confidentiality, integrity, and availability of information—often referred to as the CIA triad.

### The CIA Triad:
1. **Confidentiality:**
   - Ensures that sensitive information is accessible only to authorized users and is protected from unauthorized access.
   - Techniques such as encryption, access control, and authentication are used to maintain confidentiality.
   
2. **Integrity:**
   - Ensures that data is accurate, consistent, and has not been altered or tampered with by unauthorized individuals.
   - Methods such as hashing, digital signatures, and checksums help in preserving data integrity.

3. **Availability:**
   - Ensures that information and resources are available to authorized users whenever they need them.
   - Redundancy, failover systems, and regular maintenance are strategies used to ensure availability.

### Key Concepts in Cybersecurity:
- **Risk Management:** Identifying, assessing, and mitigating risks to digital assets, ensuring that the impact of potential threats is minimized.
- **Authentication:** Verifying the identity of users, devices, or systems before granting access to resources.
- **Authorization:** Determining whether an authenticated user or system has permission to access a particular resource.
- **Encryption:** Converting data into a coded form to protect it from unauthorized access during transmission or storage.
- **Firewall:** A security device that monitors and controls network traffic based on predetermined security rules.
- **Intrusion Detection and Prevention Systems (IDPS):** Tools that monitor networks or systems for malicious activities and take action to prevent or respond to those threats.

## 2. Types of Cyber Attacks

Cyber attacks are deliberate attempts by malicious actors to compromise the security of systems, networks, or data. Below is a detailed list of various types of cyber attacks:

### 2.1 Malware Attacks

**Malware** (short for malicious software) is any software intentionally designed to cause damage to a computer, server, client, or network. Common types of malware include:

- **Viruses:**
  - Malicious code that attaches itself to legitimate programs and spreads when the infected program is executed. Viruses can delete files, corrupt data, and cause system crashes.
  
- **Worms:**
  - Similar to viruses, but they can replicate and spread independently without requiring a host program. Worms often exploit vulnerabilities in network protocols to propagate.

- **Trojan Horses:**
  - Malicious software disguised as legitimate software. Trojans are used by attackers to gain unauthorized access to systems or to install additional malware.

- **Ransomware:**
  - Encrypts a victim's data and demands payment (usually in cryptocurrency) for the decryption key. Ransomware can cause significant financial and operational damage.

- **Spyware:**
  - Software that secretly monitors user activities, collecting sensitive information such as login credentials, financial data, or browsing history.

- **Adware:**
  - Software that automatically displays or downloads advertisements. While not always malicious, adware can be intrusive and may be bundled with spyware.

### 2.2 Phishing Attacks

**Phishing** is a social engineering attack where attackers impersonate a trustworthy entity to trick individuals into revealing sensitive information such as usernames, passwords, or credit card details.

- **Email Phishing:**
  - The most common form of phishing, where attackers send fraudulent emails that appear to be from a legitimate source, encouraging recipients to click on malicious links or download attachments.

- **Spear Phishing:**
  - A more targeted form of phishing aimed at a specific individual or organization. Spear phishing emails are often customized and appear highly convincing.

- **Whaling:**
  - A type of spear phishing targeting high-profile individuals such as executives or public figures. The stakes are higher, and the attacks are often more sophisticated.

- **Vishing (Voice Phishing):**
  - Involves attackers making phone calls pretending to be from a legitimate organization, attempting to trick victims into providing sensitive information.

- **Smishing (SMS Phishing):**
  - Similar to phishing, but conducted via text messages. Attackers send SMS messages containing malicious links or requesting sensitive information.

### 2.3 Denial-of-Service (DoS) Attacks

**Denial-of-Service (DoS)** attacks aim to make a system, service, or network unavailable to its intended users by overwhelming it with a flood of illegitimate requests.

- **Distributed Denial-of-Service (DDoS):**
  - A more powerful version of DoS, where the attack is launched from multiple compromised systems (often part of a botnet) simultaneously, making it harder to mitigate.

- **SYN Flood:**
  - A type of DoS attack that exploits the TCP handshake process by sending numerous SYN requests to a target server but never completing the handshake, causing the server to exhaust its resources.

- **Ping of Death:**
  - An attack that sends malformed or oversized ping packets to a target, which can crash or freeze the system.

- **Application Layer DoS:**
  - Targets the application layer of the OSI model, overwhelming specific applications or services (e.g., HTTP, DNS) with requests, leading to a slowdown or crash.

### 2.4 Man-in-the-Middle (MitM) Attacks

**Man-in-the-Middle (MitM)** attacks occur when an attacker secretly intercepts and relays messages between two parties who believe they are communicating directly with each other.

- **Eavesdropping:**
  - Attackers intercept communication between two parties, allowing them to listen to or read the data being transmitted, often without the knowledge of the victims.

- **Session Hijacking:**
  - An attacker takes control of a user's session after authentication, allowing them to perform unauthorized actions on behalf of the user.

- **SSL Stripping:**
  - Attackers downgrade a secure HTTPS connection to an unencrypted HTTP connection, allowing them to intercept and alter data transmitted between the client and server.

- **Wi-Fi Eavesdropping:**
  - Attackers set up rogue Wi-Fi networks or use packet sniffing tools to intercept data transmitted over wireless networks.

### 2.5 SQL Injection Attacks

**SQL Injection** is a type of attack where malicious SQL code is inserted into a query input field, exploiting vulnerabilities in an application's software to execute unintended SQL commands.

- **Union-Based SQL Injection:**
  - Attackers use the UNION operator to combine malicious queries with legitimate ones, retrieving additional data from the database.

- **Error-Based SQL Injection:**
  - Attackers trigger database error messages to gain information about the database structure, which can then be used to craft more targeted attacks.

- **Blind SQL Injection:**
  - In cases where the database doesn't return errors, attackers infer information from the database based on the application's behavior in response to true/false queries.

- **Time-Based SQL Injection:**
  - Attackers use SQL commands that trigger time delays in the database's response, allowing them to infer data based on the time it takes to respond.

### 2.6 Cross-Site Scripting (XSS) Attacks

**Cross-Site Scripting (XSS)** is a type of attack where malicious scripts are injected into web pages viewed by other users. These scripts can be used to steal session cookies, redirect users to malicious sites, or perform other unauthorized actions.

- **Stored XSS:**
  - Malicious scripts are permanently stored on a target server (e.g., in a database) and executed whenever users access the affected page.

- **Reflected XSS:**
  - Malicious scripts are reflected off a web server, usually via a URL or form input, and are executed when the user clicks a link or submits a form.

- **DOM-Based XSS:**
  - The attack occurs when the malicious script is executed as a result of modifying the Document Object Model (DOM) environment in the user's browser.

### 2.7 Zero-Day Attacks

**Zero-Day** attacks exploit vulnerabilities in software that are unknown to the vendor and for which no patch or fix is available. These attacks can be highly dangerous, as they target flaws that are not yet publicly known.

- **Exploit Kits:**
  - Attackers use tools known as exploit kits to automate the exploitation of known vulnerabilities in software, often distributing these attacks through malicious websites.

### 2.8 Advanced Persistent Threats (APTs)

**Advanced Persistent Threats (APTs)** are long-term, targeted attacks where the attacker gains unauthorized access to a network and remains undetected for an extended period. APTs are often carried out by nation-states or highly organized groups.

- **Phases of APTs:**
  - **Initial Intrusion:** Often begins with spear phishing or exploiting a vulnerability.
  - **Establishment:** Attackers establish a foothold in the network, often using backdoors or other persistent methods.
  - **Expansion:** Attackers move laterally within the network, escalating privileges and gaining access to sensitive data.
  - **Data Exfiltration:** Attackers transfer stolen data out of the network, often in small, unnoticed increments.
  - **Covering Tracks:** Attackers remove evidence of their presence to avoid detection.

### 2.9 Social Engineering Attacks

**Social Engineering** attacks manipulate individuals into divulging confidential information or performing actions that compromise security. These attacks rely on human psychology rather than technical vulnerabilities.

- **Pretexting:**
  - Attackers create a fabricated scenario (pretext) to trick individuals into providing information or performing actions.

- **Baiting:**
  - Attackers offer something enticing (e.g., free software, USB drives) to lure victims into executing malicious actions.

- **Quid Pro Quo:**
  - Attackers promise something of value (e.g., tech support) in exchange for information or access.

- **Tailgating:**
  - Attackers gain physical access to secure areas by following authorized personnel, exploiting trust or lack of attention.

### 2.10 Password Attacks

**Password Attacks** aim to steal or guess passwords to gain unauthorized access to systems or accounts.

- **Brute Force Attack:**
  - Attackers systematically try every possible combination of characters until the correct password is found.

- **Dictionary Attack:**
  - Attackers use a list of common passwords or words (a dictionary) to attempt to guess the password.

- **Credential Stuffing:**
  - Attackers use leaked or stolen usernames and passwords from one breach to attempt access on other sites or services.

- **Rainbow Table Attack:**
  - Attackers use precomputed tables of hash values (rainbow tables) to reverse cryptographic hash functions and recover passwords.

- **Keylogging:**
  - Attackers use software or hardware to record keystrokes, capturing passwords and other sensitive information as it is typed.

### 2.11 Insider Threats

**Insider Threats** involve individuals within an organization who pose a risk to the organization's security, either intentionally or unintentionally.

- **Malicious Insiders:**
  - Employees, contractors, or business partners who intentionally misuse their access to harm the organization.

- **Negligent Insiders:**
  - Well-intentioned employees who inadvertently cause security breaches through careless actions, such as clicking on phishing links or losing devices.

- **Compromised Insiders:**
  - Insiders whose accounts or devices have been compromised by external attackers, who then use them to carry out attacks.

---

Understanding these basic concepts and the various types of cyber attacks is crucial for anyone studying cybersecurity. Each attack type requires different mitigation strategies, and staying informed about new attack vectors is vital for maintaining robust security measures.
