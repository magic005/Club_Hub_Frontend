---
layout: post
title: Safe Computing - Ansh Kumar
permalink: /safecomputing
menu: nav/home.html
show_reading_time: false
---

# Safe Computing

## Privacy Risks from Data Collection  

### What is Personal Data (IOC-2.A.1)  
Personal data includes any information that can identify a person, such as names, addresses, phone numbers, emails, financial info, and browsing history.

### How and When Data is Collected  
Data is collected through actions like posting on social media, making purchases, clicking links, or filling out forms. Most of this is PII (Personally Identifiable Information) and is used for personalization, marketing, or analytics.

### Risks of Collecting Personal Data  
- Unauthorized access  
- Data breaches  
- Misuse or resale of data  
- Insider threats  
- Surveillance and privacy loss  
- Phishing attacks  
- Data persistence  
- Identity theft

### How to Prevent Privacy Violations  
- Encrypt data  
- Use multi-factor authentication (MFA)  
- Minimize the data collected  
- Keep systems updated  
- Use access control  
- Avoid password reuse  
- Comply with laws like GDPR, HIPAA, CCPA

### Popcorn Hack: Identify PII  
Answer: A. Fingerprint

---

## Safe Computing – IOC-2.B  

### IOC-2.B.1: Authentication Measures  
MFA protects against unauthorized access by requiring multiple factors:  
- Something you know (password)  
- Something you have (code/device)  
- Something you are (biometrics)

### IOC-2.B.2: Strong Passwords  
A strong password is long, random, and unique. Use 8+ characters, mix letters, numbers, symbols, and avoid reusing passwords across sites.

### IOC-2.B.3 & 2.B.4: MFA and Security Layers  
MFA adds extra security beyond passwords. Even if one factor is compromised, other layers prevent full access.

### Pop Quiz: Multifactor Authentication  
Question: Which of the following is NOT an example of MFA?  
Answer: D. A username required to log in

### IOC-2.B.5: Encryption  
- **Symmetric encryption**: One key for both encryption and decryption  
- **Public key encryption**: Public key encrypts, private key decrypts

### Popcorn Hack: Encryption Quiz  
Answer: B. Finn and Gwen use a shared key to encrypt/decrypt symbols.

### IOC-2.B.6: Certificate Authorities  
CAs issue digital certificates (like SSL/TLS) to verify website authenticity. Certbot is an open-source tool for managing certificates and enabling HTTPS.

### IOC-2.B.7: Antivirus and Malware Protection  
Antivirus uses signature-based detection, heuristics, and real-time monitoring. Keep it updated, use real-time protection, and avoid sketchy downloads.

### IOC-2.B.11: Privacy and Permissions  
Review app permissions. Avoid apps that request unnecessary access. Disable camera/mic/location access when not needed.

---

## Safe Computing – IOC-2.C  

### IOC-2.C.1: Phishing  
Tricks users into giving personal info (emails, texts, fake logins). Don’t click unknown links or reply to suspicious messages.

### IOC-2.C.2: Keylogging  
Records everything typed. Often hidden in malware. Avoid by not installing untrusted software.

### IOC-2.C.3: Data Interception  
Happens over insecure networks or rogue WiFi. Includes passive (reading) and active (altering) interception. Always use secure connections (HTTPS).

### IOC-2.C.5: Malicious Links  
Links may redirect to fake sites or install malware. Found in ads, emails, or websites. Don’t click unless verified.

### IOC-2.C.6: Malicious Emails  
Can contain harmful links, files, or impersonate someone you know. Don’t open unknown attachments or click suspicious email links.

### IOC-2.C.7: Freeware  
Free software can be bundled with malware. Don’t install from unknown sources or sketchy sites.

### Real-Life Example  
Connected to fake WiFi named “WiFi Coffee Shop Free” instead of real one. Used HTTP, so attacker intercepted data via rogue access point. They could read or manipulate the data. Emphasizes using HTTPS and verifying WiFi networks.

### Popcorn Hack: Password Security  
Used security.org to test a strong password. Good passwords are long, random, include symbols, and are unique across sites.