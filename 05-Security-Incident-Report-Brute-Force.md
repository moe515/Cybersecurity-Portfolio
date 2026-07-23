# Security Incident Report: Brute Force Attack
## yummyrecipesforme.com

---

## Section 1: Network Protocol Identified

The network protocols identified in the tcpdump log are **DNS** and **HTTP**.

- **DNS** was used to resolve the domain names yummyrecipesforme.com and greatrecipesforme.com
- **HTTP** was used to establish the connection between the browser and both websites on port 80

---

## Section 2: Incident Documentation

At 14:18, a DNS request was made for yummyrecipesforme.com and the browser successfully connected via HTTP. The website prompted the user to download an executable file. After running the file, at 14:20, a DNS request was made for greatrecipesforme.com, and the browser was redirected to the malicious website.

Investigation revealed that a former employee conducted a brute force attack on the admin panel by repeatedly guessing the default password until access was gained. The attacker then modified the website's source code by embedding a JavaScript function that forced visitors to download malware. After embedding the malware, the attacker changed the admin password to prevent the website owner from regaining access.

Customers reported that after running the downloaded file, their browsers were redirected to greatrecipesforme.com and their computers began running slowly.

**Evidence sources:** tcpdump traffic log analysis and source code review by senior analyst.

---

## Section 3: Recommendation

**Implement Two-Factor Authentication (2FA)** on the admin panel.

This prevents unauthorized access even if the password is compromised through a brute force attack, because the attacker would also need a second verification method to log in. 2FA should be implemented immediately and maintained permanently as a standard security measure.
