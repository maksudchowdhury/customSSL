# Custom Self-Signed SSL: Automated Certificate Generation for Secure Web Servers

This project demonstrates my ability to build a secure web server from scratch, focusing on **cybersecurity** practices such as **SSL/TLS encryption**. I utilized **OpenSSL** to create a **self-signed certificate authority (RootCA and SubCA)** and generate server SSL certificates. The process was fully automated using Linux shell scripting, showcasing my proficiency in both **Linux** and **cryptography**.

[![Watch the video](https://img.youtube.com/vi/2AdqcC8hQNI/0.jpg)](https://www.youtube.com/watch?v=2AdqcC8hQNI)

Click above to watch a full walkthrough of the project on YouTube.

---

## Project Overview

In this project, I accomplished the following:

- Built a **custom web server** with enhanced security using SSL/TLS encryption.
- Generated **RootCA, SubCA**, and **server SSL certificates** using **OpenSSL**.
- Scripted the entire setup to **automate folder creation**, **key generation**, and **certificate signing**.

## Linux Shell Script Overview

The shell script automates:

1. **Folder Setup:**

   - Creates the necessary directory structure for the RootCA, SubCA, and server certificates.
   - Initializes files like index and serial numbers for certificate tracking.

   ```bash
   mkdir -p {root-ca,sub-ca,server}/{private,certs,index,serial,pem,crl,csr}
   mkdir generated
   touch root-ca/index/index
   touch sub-ca/index/index
   ```

2. **Key & Certificate Generation:**

   - Generates private keys for the RootCA, SubCA, and server.
   - Creates and signs certificates with respective configurations.

   ```bash
   openssl genrsa -aes256 -out root-ca/private/ca.key 1024
   openssl req -config root-ca/root-ca.conf -key root-ca/private/ca.key -new -x509 -days 7305 -sha256 -extensions v3_ca -out root-ca/certs/ca.crt
   ```

3. **SSL Certificate Creation:**

   - The SubCA signs the server SSL certificate, ensuring a proper certificate chain.

   ```bash
   openssl req -key server/private/server.key -new -sha256 -out server/csr/server.csr
   openssl ca -config sub-ca/sub-ca.conf -extensions server_cert -days 365 -notext -in server/csr/server.csr -out server/certs/server.crt
   ```

4. **Packaging and Export:**

   - Gathers all relevant certificates and keys into a single directory for easy deployment.

   <br>

   ```bash
   cp root-ca/certs/ca.crt generated
   cp server/certs/server.crt generated
   cp server/private/server.key generated
   ```


## Skills Demonstrated

- **Linux Scripting:** Automated the certificate creation process with shell scripting.
- **OpenSSL Proficiency:** Generated secure SSL/TLS certificates with custom configurations.
- **Cryptography Knowledge:** Applied encryption techniques to secure web communications.
- **Cybersecurity Practices:** Implemented essential practices to enhance web server security.

## How to Run

1. Clone this repository.
2. Modify the configuration files (`root-ca.conf`, `sub-ca.conf`) as needed.
3. Run the provided shell script to generate your own RootCA, SubCA, and server certificates.

---

[![Watch the Video](https://img.shields.io/badge/Watch-Video-red?style=for-the-badge)](https://www.youtube.com/watch?v=2AdqcC8hQNI)
