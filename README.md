Analysis and Cracking of WPA2-PSK with Subsequent Data Extraction from a Certificate

In this project, I demonstrated vulnerabilities in the security of wireless networks (WPA2-PSK) and certificate files (PFX). Using Kali Linux tools, I performed the following tasks: capturing and analyzing Wi-Fi traffic, cracking the WPA2 password using a dictionary attack, and decoding and extracting data from an encrypted certificate.

To capture and analyze Wi-Fi traffic, I used the VanSpy.pcapng file containing captured Wi-Fi traffic. The tools employed were hcxtools, hashcat, and Wireshark. The first step was converting the .pcapng file to the .hc22000 format required for the attack using the command hcxpcapngtool -o outputfile.hc22000 VanSpy.pcapng. Next, I launched a password attack using the rockyou.txt dictionary with hashcat -m 22000 outputfile.hc22000 /usr/share/wordlists/rockyou.txt. As a result, the password for the FreeWifiBFC network was successfully cracked: KEY FOUND! [ Christmas ].

Moving on to working with the PFX certificate, I processed an encrypted certificate in Base64 format using OpenSSL and base64. The first step was decoding the Base64 string into a binary .pfx file with echo 'MIIJuQIBAzCCCXUGCSqGSIb3DQEHAaCCCWYEggli...' | base64 -d > cert.pfx. Then, I extracted the private key from the certificate using openssl pkcs12 -in cert.pfx -nocerts -out rdp_key.pem -nodes. The certificate password was entered during execution. As a result, I obtained the rdp_key.pem file containing the private key, which can be used for authentication in services such as RDP or HTTPS.

The project highlighted several key vulnerabilities. The WPA2-PSK password Christmas was cracked in seconds, demonstrating the importance of using strong passwords and protection against dictionary attacks. Additionally, successfully extracting the key from the PFX file exposed the risks of sensitive data leakage in Base64-encoded formats.

Based on the work performed, I concluded that using WPA3 and complex passwords for Wi-Fi is essential to minimize security risks. Encrypting certificates and restricting access can prevent data leaks, and monitoring network traffic can help detect anomalies in a timely manner.

All steps were documented in the Kali Linux terminal. The tools used included hcxtools and hashcat for WPA cracking, OpenSSL for working with certificates, and rockyou.txt, a standard Kali Linux dictionary. This project was conducted solely for educational purposes to study protection methods and attacks on network protocols.

