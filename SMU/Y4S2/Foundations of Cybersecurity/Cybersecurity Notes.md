# Basics
### TCP/IP Protocol Suite
- Application 
- Transport  
- Network 
- Data link 
- Physical
### Router 
- stores and forwards IP packets, based on a routing table
- key functions:
	- run routing algorithms/protocol
	- forwarding network packets from incoming to outgoing link
### Threat, Vulnerability, Attack & Incident
- Threat: something bad that could happen
- Vulnerability: weakness in an information system that could be exploited
- Attack: some action taken by a malicious intruder
- Incident: when a vulnerability is exploited to compromise the security of systems, the result is a security incident
### Classical Security Properties
- Integrity: Information is not modified by unauthorised parties
- Availability: Information can be accessed by authorised parties at proper time
- Confidentiality: Information is not exposed to unauthorised parties
#### Other Important Properties
- Accounting: the ability of a system to keep track of what users do while they are logged into a system
- Non-repudiation: the ability of a system to ensure that a sender cannot convincingly deny having sent something
- Authentication
- Authorization
# Symmetric Encryption

### Rationale of Encryption
Goal: to make the ciphertext without patterns recognisable to the adversary
 - Approach 1: substitution
 - Approach 2: shuffle or permutation
### One-Time Pad (a.k.a Vernam Cipher)
Plaintext P is encrypted and decrypted using a XOR operation on a key K with the same length as the plaintext P
- considered to achieve _[unconditional security](unconditional%20security.md)_ without knowing K (K is unique for every P)
- **Impractical:** need for synchronisation and unlimited number of keys
### Block Ciphers
- Encrypt binary messages in chunks (blocks)
	- Text messages are also in binaries when they are processed by computers
- A block is a fixed number of consecutive bits in the message
- To encrypt a message, map each block in the message to another block chosen from the block domain (i.e. the set of all possible blocks)
- The cipher algorithm and the key jointly define the mapping between plaintext blocks and ciphertext blocks
### Symmetric (Key) Encryption
- DES - 56bits of key
- 3DES
- AES key size - 128, 192, 256 bits
- AES block size - 128 bits
### Modes of Encryption
- AES is symmetric key encryption method
- Two modes to encrypt messages
	- ECB: Electronic Code Block
	- CBC: Cypher Block Chaining
> The block cipher key only specifies the plaintext-ciphertext block mapping. It does not deal with the relation among blocks, i.e. mode of encryption
#### ECB Mode
Each cipher block is encrypted from the same corresponding block
BLK1 -> CBLK1, BLK2 -> CBLK2, BLK3 -> CBLK3
- Not random and very predictable
#### CBC Mode
- Before applying AES upon the plaintext, a random block is chosen as the initial vector (IV)
	- length of IV is the same as the block size
- IV needs NOT be a secret, and is known to both the sender and the receiver  
- **Purpose of the IV is to introduce randomness into the encryption process**
	![|600](images/Pasted%20image%2020240116101619.png)

|  | ECB mode | CBC mode |
| :--- | :--- | :--- |
| **Identical plainext blocks result in ** | identical ciphertext blocks | different ciphertext blocks |
| **chain dependency** | blocks are enciphered independently | proper encryption/decryption requires a correct preceding plaintext/ciphertext block |
| **error propogation** | none | a ciphertext block’s error affects decipherment of itself and the next block. |
### Cryptanalysis
- Objective: Given a ciphertext, find its plaintext
- Assumption: attacker knows encryption method E and decryption method D
![||600](images/Pasted%20image%2020240116104714.png)
### Frequency Analysis
 - If a cipher preserves the pattern of the plaintext, it is susceptible to the ciphertext-only attack by applying frequency analysis
- used against substitution ciphers
- based on the idea that certain letters occur with varying frequencies. And such frequencies of letters are preserved in the ciphertext
### Moore's Law
 - Computing (processing) power doubles every 18 months while the costs of integrated circuits stay constant
### Troubles of Secret Key Distribution
Pair-wise secure communication among n users: 
- n(n-1)/2 different secret keys in total
- n-1 secret keys stored by each user
#### Issues
- Requires a SECURE key distribution channel
- Not scalable (key management problem)
# Asymmetric Encryption
RSA encryption setting consists of three parameters
- **n**: a composite integer, **n=pq** where **p** and **q** are very large primes
- **e**: an integer co-prime to **(p-1)(q-1)**
	- co-prime: e and (p-1)(q-1) do not have a common divider except 1
- d
(n, e) are called the RSA public key, n is called the RSA modulus, d is the RSA private key
### Notation $a\equiv b\ (mod\ n)$
**Definition**: Let a, b, n be three integers. a is **congruent** to a **modulo n** if and only if a and b 

### Using RSA 
- RSA encryption is performed only on integers smaller than the RSA modulus, M<=n
- Encryption formula to encrypt M, compute $M^e mod\ n$ as C (ciphertext)
- Decryption formula to decrypt C, compute $C^d mod\ n$ as M (plaintext)
### RSA deterministic Problem
RSA is deterministic because the attacker may choose likely plaintexts and pre-encrypt using the known public key then test if they are equal to the chosen ciphertext. If a match is found, a corresponding plaintext to a stolen ciphertext is recovered
> chosen plaintext attack
### RSA with Random Padding
use random padding R and encrypt with P and R together
- Encryption of P: $C = (R||P)^e mod\ n$ 
- Decryption of C: $(R||P) = C^d mod\ n$
	- Public key cryptography standard (PKCS): R is 34 bytes
	- If n is 2048 bits (256 bytes), then P should be at most 256-34=222 bytes so that (R||P) is 256 bytes
	- Therefore, RSA is only appropriate for encrypting small-size data
### RSA Key Size and Security
It is common to choose n to be 2048 bits 
- Security depends on difficulty of solving factorisation problem to get p and q from n

| Asymmetric Encryption | Symmetric Encryption |
| ---- | ---- |
| Public keys can be sent over a public channel | A secret key must be distributed over a secure channel |
| Scalable for multi-party communication | Non-scalable for multi-party communication |
| Long keys | Relative short keys (e.g. 128 bits) |
| Slow encryption speed | Fast encryption speed |
### Limitation of RSA encryption
- trouble in encryption large files -> when being converted to an integer, it may be bigger than the RSA modulus in use and cannot be encrypted directly
### Envelope encryption
A hybrid of public key (asymmetric) encryption and symmetric encryption
##### Encryption
- Select a random symmetric key k, e.g. an AES key
- Use k to encrypt message m, to get ciphertext C1
- Use RSA public key to encrypt k, to get ciphertext C2
- Send (C1, C2) to receiver
##### Decryption
- Use RSA private key to decipher C2 to get k
- Use k to decipher C1 to get m

Hybrid encryption is in essence a message encryption combined with an RSA-based secret key distribution

# Message Integrity and Authentication
### Message Integrity technique
- Send a small piece of information as a proof of message integrity so that the counterparty can use it to detect attacks to message integrity
- Sender sends a hash value along with message 
- Receiver computes the hash value from the message using the hash function to evaluate the integrity of the message
### Proof of Message Integrity
- Symmetric proof
	- Message authentication code (MAC) / HMAC
- Asymmetric proof
	- Digital signature / RSA signature

Both MAC and Digital signature are constructed based on a hash function
### Hash Function
- maps data of arbitrary size to fixed-size values
- Hash value **h=H(M)** is also referred to hash, digest, or message digest
- Hash function can be MD4, MD5, SHA1, SHA2, or SHA3
#### Standard Hash: SHA
- SHA1: 160bits
- SHA2:
	- SHA2-224, SHA2-256, SHA2-384, SHA2-512
- SHA3
	- Keccak-224, Keccak-256, Keccak-384, Keccak-512
#### Three properties of secure secure hash function
1. One-way
	- easy to compute but hard to inverse (non-reversible function)
	- **Pre-image attack**: attacker tries to find an input (pre-image) that corresponds to a specific hash value
2. Collision resistant (sensitive to change)
	- hard to find M != M' such that M(M) = H(M')
	- **Collision attack**: find M = M' such that H(M) = H(M')
		- message M and M' both results in the same hash
		- easy to forge message M' as a valid message due to the same hash result
3. Fixed length (|h| is fixed)
	- variable length of M -> fixed length of h
	- |h| is typically small 
## Message Authentication Code (MAC)
A tag used to authenticate the message and verify the message integrity
### HMAC (A type of MAC)
- Alice and Bob share a secret key K. (pre-requisite of using HMAC)
- Alice send message (M, δ)
- MAC = H(K || M || M’) 
- HMAC = H ( K || (H(K||M) )
- δ is computed as MD5(K || MD5(K||M)), “K||M” means the concatenation of the binary strings of K and M.
- Bob receives (M, δ).
- To verify the integrity, he computes his own version of HMAC in the same way as Alice. If the outcome equals δ, the message is intact. 
- A third party that does not know the secret key K cannot manipulate the HMAC
### HMAC vs Hash
- **Hash Functions:** Provide a one-way transformation of data and are used for various purposes, including integrity verification
- **HMAC:** Specifically designed for message authentication using a keyed hash function, providing both integrity and authenticity
- **Security:** HMAC offers a higher level of security for authentication purposes due to its key-based construction
> Inclusion of secret key k ensures authenticity for message M, because we know about the originator of the message, based on the shared secret key. There is no way to provide authenticity for a message m solely with hashing alone
### Repudiation Problem
- If the counterparty denies the fact that they have sent message M and MAC to the sender, the sender cannot provide to any third-party authority that the counterparty is lying
	- This is because both the party and counterparty can generate the MAC value from M as they share the MAC key
	- The counterparty can accuse party of generating MAC=H(k, M) by themself
#### Limitation of HMAC
- the need of a secure channel to exchange a shared secret
- inability to provide non-repudiation

> MAC is a keyed hash function 
> MAC provides both integrity and authentication
> MAC does not provide confidentiality
## Digital Signature
- Uses asymmetric cryptography
- Provide authenticity and integrity services for messages transmitted through a non-secure (public channel)
- Also provide non-repudiation service
- Equivalent to traditional handwritten signatures and typically more difficult to forge than handwritten signature
### Signing
- Alice generates RSA public key (e,n) and private key d
- Alice computes digital signature sig on her message M
- Sig = $H(M)^dmod\ n$ 
- Note that this sig for M can only be generated by Alice with her private key d
- Alice sends both message and signature (M, sig) to Bob over a public channel
### Property of asymmetric cryptosystem
Given a pair of public key (e,n) and private key d
- When you compute x with one of the keys as follows:
	- x = ye mod n [encryption]
- You (can) get back y (only) when you use the other key as follows:
	- y = xd mod n [decryption]
- Signing:
	- sig = $H(M)^dmod\ n$ 
- Verifying:
	- $H(M) = sig^emod\ n$
### Verification
- The party, upon receiving (M, sig):
	- computes $H(M_{received})$ by hashing the received $M$
	- computes $H(M)=sig^emod\ n$ using the received $sig$
	- verifies integrity of message M by comparing $H(M_{received})$ against $H(M)$
	- verification passes if $H(M)$ and $H(M_{received})$ match; fails otherwise
- **Note that not only the party but also anyone can verify $(M, sig)$ using the counterparty's public key $(e, n)$**
### RSA signatures vs. encryption
|  | RSA Signatures | RSA Encryption |
| ---- | ---- | ---- |
| **Objective** | data integrity, data authentication | data confidentiality |
| **Requirement of private key from sender** | Yes, must have the private key to sign the message | No, don't need to have any secrets |
| **Requirement of private key for the receiver** | No, everyone can verify | Yes, the decryption requires the private key |
| **Limitation of data size** | No limitation, can sign any file | Yes, only encrypt data smaller than the modulus |
### RSA signatures vs. HMAC
| RSA Signatures | HMAC |
| ---- | ---- |
| data integrity, data authentication | data integrity, data authentication |
| Non-repudiation. The sender cannot deny | The sender can deny |
|  Everyone can verify | Only the sender and the intended receiver can verify because they share the secret key |
| Slow due to big number computation | Fast |
# Public Key Infrastructure (PKI)
Public key certificate:
- a digital token issued by an (trusted authority) to certify the ownership of a public key
Public key infrastructure
- Core idea: Certificate Authority (CA) issues certificates to public-key holders
### Public Key Certificate Components
- If someone modifies the certificate, verification will fail because the signature will be different
- If someone replaces the certificate, verification will fail because identities (e.g. website IP, email addresses) are different
**Mandatory components**
- Subject identifier
- Issuer's identifier
- Owner's (subject's) public key info
- Validity period
- CA's signature
## Certificate Request and Issuance
### Certificate Issuance
What should the sender send to the CA?
- Alice's RSA public key (n,e) and private key d
- Alice’s certificate request is Alice’s signature on her public key using her private key.
	- Let M be the message consisting of n and e.
	- Alice -> H(n||e)d mod n -> (Sig, (n,e)) -> CA
	- CA -> check if H(n||e) == Sige mod n ? (digital signature verification)
- If the signature (M,sig) is valid, the request is approved
	- CA is convinced Alice knows d. Otherwise she cannot sign.

1. CA checks Alice’s identity (actual cost of using public key infrastructure) and verifies Alice’s request using the public key being signed.
2. If both are correct, CA issues a certificate for Alice’s public key in the following steps:
	1. Construct the certificate body consisting of the key elements shown in Yeow Leong’s Certificate example.
	2. Sign the certificate body (M) with CA's private key -> H(M)d mod n
	3. Alice's certificate = certificate body + CA's signature

### Certificate Verification
- A public key certificate is publicly verifiable, i.e. it can be verified by anyone.
- A user obtains an entity’s (e.g. web server) certificate, either by receiving it from the entity or retrieving it from some directory.
- To verify Alice’s certificate, Bob runs the following steps:
	1. If it has expired, return false; otherwise,
	2. verify the signature of the certificate with the certificate body using CA’s public key. If invalid, return false;
	3. verify whether CA’s public key in use is trusted. If positive, return true; otherwise return false.
### Certification Chaining
- CA is certified by another CA
- CA's CA is certified by another CA
- CA's CA's CA is certified by...
#### Root CA
- A root CA can certify itself by signing on its own public key PKCA using its private key PrKCA so as to produce a self-signed certificate CertCA =(CA, PKCA ,… SigCA).
- Most browsers pre-load many popular root CAs’ certificates (which are self-signed)
#### Trust or Not Trust?
Two approaches for trust establishment
- Most browsers have pre-loaded those root CA certs which are widely considered as trusted, such as Microsoft, Verisign’s root CA certs.
- You can manually instruct the browser to trust a root CA’s certificate, by installing the certificate in the browser
### Certification Revocation
If a private key is compromised, ideally its corresponding public key should not be used any longer
Basic idea of revocation:
- The authority periodically publishing a blacklist of those revoked certificates' serial numbers
- the blacklist is called Certificate Revocation List (CRL)
- It is the user's burden to download the latest CRL

A Certificate Revocation List is a **signed** list issued by CA, which contains the serial numbers of revoked certificates
### Certificate Verification with CRL
To verify Alice’s certificate Cert={Alice, PKAlice, …, SigCA(Alice, PKAlice, …)}, Bob runs the following steps:
1. Check if it has expired or not. If not,
2. Verify the signature SigCA(Alice, PKAlice, …) using CA’s public key.
3. Verify the entire certification chain;
4. Check whether Alice’s certificate is in the CRL

Step 4 is not strictly enforced, because of performance and privacy issues
### SSL/TLS Protocol
- TLS provides
	- Implicit server authentication (because the server has a public key certificate)
	- A secure channel between the server application and the client application (to encrypt/authenticate data sent in between).
- TLS runs in two phases
	- Handshake
	- encryption and/or data authentication, integrity
#### Handshake
- Server sends it public key certificate to the client. The cert contains the Server's public key (e.g. RSA public key)
- Client
	- generate a random secret key k (e.g. an AES key)
	- encrypt k with Server's public ket
	- send the ciphertext to Server
- Server decrypts the ciphertext to get k
- Hereafter, Server and Client use k to protect their communications
	- encrypt messages using k for confidentiality
	- use HMAC to protect integrity
# User Authentication & Identity Management
**Identification** is the act of asserting who the subject is

**Authentication** is the act of proving that asserted identity, that is, the subject who it says it is

**Subject** are people, computer processes (executing programs), network connections, devices, and similar active entities
- What you have 
- What you know 
- What you are
#### Weak and Strong Authentication
User authentication: based on a shared secret S
- Weak authentication: Bob proves his identity to the server by revealing knowledge of S
- Strong authentication: Bob does not reveal S but he proves that he knows S
## Weak Authentication
- Bob sends Server unencrypted password 
	- Requires secure channel
- "Encrypted" password file
	- Exposure of password file leads to password exposure
	- Need to protect the decryption key
### The Right Approach
- Initialisation: Server chooses an arbitrary message M (e.g. M is a string of 64 0-bits) and creates a password file
- To register a user, Server inserts a new record into the password file. The record consists of two items:
	- User id
	- A ciphertext obtained by encrypting/hashing M using the user's password
- Server's verification procedure
	- encrypt/hash M using the submitted password to get a ciphertext
	- compare the result against the corresponding record in the password file

> **Advantage**: Server does not store any secret; Server does not keep the users' password
### Attack on passwords
- Based on whether to involve the authentication Server
	- Online attack: Server is involved during attack
	- Offline attack: Server is not involved during attack
- Based on how to guess:
	- Brute-force attack: guess randomly
	- Dictionary attack: guess from a dictionary = a list which contains most commonly used passwords
#### Online/Offline Attacks
Online attacks can be easily countered by
- Choosing long password (from user/server point of view)
- Limiting the number of tries (from server point of view)
- Slowing down log-in process
Offline attack
- Adversary (with the help of some automated tool)
	- Obtains the encrypted password file
	- Tries every possible password and encrypt/hash it
	- Compares the ciphertext of each tried password to all passwords in the password file
- Does not involve the authentication server
#### Dictionary Attack
- Looks for a match between the pre-computed password file and the real password file
> Dictionary attacks are fast, but only work for **weak passwords**
### Salt
- If two users use the same password, it will have the same encrypted/hash value
- Subject to Dictionary attack
- Add an extra data value unique for each user, called the *salt* value
### Drawbacks of Weak Authentication
- The user has to reveal her secret. It implies that user and the server MUST use an encrypted channel (i.e. the communications are encrypted)
- Password authentication is subject to replay attacks
	- the user always submits the same information (i.e. username & password)
	- **Replay attack**: The attacker can re-send whatever the user has sent in prior authentication sessions, without knowing the actual data
## Strong Authentication
### One-Time Password Scheme
- Strong Authentication: the user does not reveal her secret to the server
- Objectives:
	- to defeat replay attacks
	- to remove the need for a secure channel
- Two methods for strong authentication:
	- challenge-response protocol
	- time-stamp protocol
### Challenge-Response Protocol
- Server and Bob share a secret key K
1. Upon authentication request, Server sends Bob a **random** challenge C
2. Bob responds with $R_b=Enc_K(C)$ or $R_b=Hash(K||C)=HMAC$
3. Server computes $R_S$ in the same ways as Bob does. If $R_S=R_b$, Bob is authenticated successfully
### Time Stamp Authentication Protocol 
- Server and Bob keep synchronised clocks and a shared key K
	- Time is used as one-time "challenge"
1. Bob sends Server his id, and $R=Enc_K(T)$ with his clock reading T
2. Server verifies whether $T=Dec_K(R)$ using Bob's key K and its own clock reading T' within the same window
	- If |T'-T| < window size, the verification is successful
#### How the hash function is used in Time Stamp Protocol
1. Bob sends Server his id, and $R=HMAC_k(T)$ with his clock reading T (T is taken at a predefined discrete interval, e.g. 30s interval)
2. Upon receiving R, Server computes a few HMAC values (depending on the time window)
	- For example, $HMAC_k(T')$, $HMAC_k(T'-30)$, $HMAC_k(T'-60)$
	- If one of the computed HMAC values match against R, Bob is authenticated
### Comparisons
Challenge-response
- 3 message flows
- needs to generate a random number
Time stamp 
- 1 message flow
- time synchronisation is difficult
- a time window for attacks
	- because a response is valid within a time window, the eavesdropper can reuse the response within that time window
### Single Sign-On for Web Services
- User log in once per session
- Single Sign-On Trusted Third Party (TTP) maintains your identities and authentication codes for all the different, independent applications
- When user wants to access an application, TTP handles authentication on behalf of the user
### SAML
- Security Assertion Markup Language
- Users can gain access to websites in multiple domains without having to re-authenticate after initially logging in to the first domain
- Domains need to form a trust relationship before they can share an understanding of the user's identity
#### Asserting Party
- SAML expresses assertions about a subject that other applications within a network can trust
- Asserting party (SAML authority): system or administrative domain that asserts information about a subject
- Asserts that a user has been authenticated and has been given associated attributes
#### Relying Party
- System or administrative domain that relies on information supplied to it by the asserting party 
- It is up to the relying party as to whether it trusts the assertions provided to it
	- Trust: assertion really comes from the asserting party
	- Local access policy defines whether a subject may access local resources 
# Access Control
The process of specifying and controlling who (**which subjects**) can access what (**which objects**) and how (**by which means**) is called **access control**
### Three Models
- Discretionary Access Control (DAC): the access rights are at the discretion of the resource owner
- Mandatory Access Control (MAC): the access rights are mandatorily defined based on certain policies, not at one's discretion
- Role-Based Access Control (RBAC): the access rights are defined according to the users' roles
- **In general, an access control model involves three elements: subject, objects, rights**
#### User - Principal
- One to many mapping between user and principals
- System authenticates user in the context of principal
- Shared principals (accounts) are not good for accountability
- **A principal represents the identity and role/group of the user and acts on the user's behalf**
#### Principal - Subjects
- One to many mapping between principal and subjects
- A subject is a program or application running on behalf of the principal
- If all subjects of a principal have the same rights, they are often treated same as principal
#### Objects
- An object is anything on which a subject can perform operations (mediated by rights)
- Usually objects are passive: file, directory, memory segment
- But, subjects can also become objects, with operations: Kill, Suspend, Resume
#### Rights
- specifies what kind of access a subject can perform on an object
- typical rights include: own, read, write, execute
## Discretionary Access Control (DAC)
- Logically, DAC can be represented as an access control matric (ACM)
- It is inefficient to implement ACM directly. ACM might be sparse
### Access Control List
- ACL - Each column of access control matrix is stored with corresponding objects
- ACL requires subjects to be authenticated before making the decision
## Mandatory Access Control (MAC)
- Access control policies in DAC are defined according to the owner's **discretion without rigorous security checking**
	- It may have security loopholes leading to trojan horse attack that leaks confidential information
		- Principal V sends U a software with Trojan horse embedded
		- U executes the software -> Trojan horse has U's privileges
- MAC augments DAC using security labels attached to subjects and objects
	- Security label to subject -> security clearance
	- Security label to object -> security classification
- Information flow strictly follows those paths satisfying policies predefined according to labels
- Users cannot create/modify security labels which are assigned by Admin only
- **Key idea**: classify subjects and objects, and define policies on information flow
### Label Hierarchy
![|600](images/Pasted%20image%2020240220100736.png)
There is an order among labels, it's a **total** order. If any two labels are comparable; otherwise, it is **partial** order
### BLP Model
Bell and LaPadula model (BLP)
- A formal MAC model which lays out the rules for concrete access policies based on security labels
- The principles define allowable information flows in order to maintain data secrecy (confidentiality)
- Does not address integrity
#### Two MAC Rules
- Simple-security property (read-down)
	- Subject S can read object O only if label(O) is lower than or the same as label(S)
- Star-property (write up)
	- Subject S can write object O only if label(O) is higher than or the same as label(S)
> ACL: AC decisions are made based on principals
> ACL + BLP: AC decisions are made based on principals + security labels of subjects and objects
### Downsides of MAC
- not appropriate for some commercial use; originally designed for military use
- there are significant differences between commercial and military information security
	- Data items (objects) may have different degrees of sensitivity: public, proprietary, internal
	- No formalised notion of clearances (subjects) -> no dominance (can-flow) function -> access is less regulated
## Role-Based Access Control (RBAC)
A general access control model for management of security in companies and organisations
- General, flexible and easy-to-use
- Support at application level 
### Flexible Security Management
- Security management is simpler with RBAC
	- User-role relationship changes over time
	- Role-permission relationship is relatively stable
	- Security management based on roles rather than permissions is simpler
# Network Security
### IP Packets or Datagram
- **Internet Protocol (IP)** Address: 4 bytes or 32 bits, usually in dot decimal notation, used by network interfaces
- Most IP addresses are publicly accessible in the internet. Some are for private addresses, i.e. they cannot be **directly** reached in the internet, e.g. the SMU IP address assigned to your computer
- **Ports**: 
	- two bytes or 16 bits, used by applications within one device
	- There are two types of ports: TCP ports and UDP ports. The uses of them follow different protocols
- Internet communications are in the form of a stream of packets which usually specify four addresses: source IP, destination IP, source port, and destination port
- 32-bit IP address
	- Network-layer address
	- Used to get datagram to destination host
- MAC address 
	- Also called LAN or physical or Ethernet address
	- Used to get link layer frames from one interface to another physically-connected interface (same subnet)
	- 48 bit MAC address (for most LANs) burned in the adapter ROM
### ARP: Address Resolution Protocol
- Each IP node (Host, Router) on a LAN has an ARP table
	- ARP table: IP/MAC address mappings for some LAN nodes < IP address; MAC address; TTL
	- TTL (Time To Live): time after which the address mapping will be forgotten
##### Example Flow
1. A wants to send datagram to B, and B's MAC address is not in A's ARP table
2. A broadcasts ARP query, containing B's IP address
	- Dest MAC address = FF-FF-FF-FF-FF-FF
	- All machines on LAN receive the ARP query
3. B receives the ARP query, replies to A with its MAC address
	- Frame sent to A's MAC address using unicast
4. A caches (saves) the IP-MAC address pair in its ARP table until information times out
5. ARP is "plug-and-play" 
	- Nodes create their ARP tables without intervention from the network administrator
### Denial of Service Attack
- Overwhelm the victim to the point of unresponsiveness to legitimate users
- By carefully constructing a sequence of packets with certain characteristics
- An intruder can cause vulnerable systems to crash, hang, or behave in unpredictable ways
### Network Firewall
- Main functions: by filtering and auditing traffic between internal and external network
	- Prevent unauthorised access to a private network and unauthorised outgoing traffic
	- Traffic volume/speed regulation
- Deployed at the network boundary
#### Firewall categorisation
- Policy
	- Close policy: only whitelisted packets are forwarded
	- Open policy: only blacklisted packets are dropped
- Functioning level
	- IP layer: packet filtering gateway
		- makes decision based on individual packet
		- examine packet headers (i.e., metadata) only
	- Application layer: Application proxy gateway (bastion host)
		- inspect the contents of communication by simulating the effect of the application
- Position
	- Network based: Network Based Firewall filters traffic going from internet to secured LAN and vice versa
	- Host based: a host based firewall is a software application or suite of applications installed on a single computer, to provide protection to the host
#### Limitations of Firewall
- Single Point of Failure
- Performance bottleneck
### Intrusion Detection System (IDS)
- Main function: inspect network traffic within a network to detect attacks
- An ideal IDS should notify security manager of an ongoing attack
	- 100% accuracy
	- In real time manner
	- Complete diagnosis
	- Effective recommendations on how to react
#### Signature-Based vs Anomaly-Based
##### Signature based IDS
- basic idea: to match network traffic with pre-defined attack patterns (i.e., signatures)
- e.g., signature of code red worm
- Good: Low false alarm rates, instantaneous detection (practice)
- Bad: Cannot detect new attacks (a.k.a. 0-day attacks)
##### Anomaly based IDS
- profile: model of normal behaviours
- IDS reports situations that deviates from profiles
- basic idea: IDS has been trained to differentiate normal traffic and abnormal traffic, by using machine learning techs
- Good: Can detect some new attacks
- Bad: High false alarm rates, high complexity (research)
#### Behaviour Modelling
- Sliding windows of size k+1 (e.g., k=3)
![|600](images/Pasted%20image%2020240414161247.png)
- Number of mismatches = 5
- Max number of mismatches = 18
- Miss rate = 5/18 = 27.8%
> Sliding window to match left's given input to right's correct sequence. Anything not conforming to the list is an anomaly
#### Assumptions
- A compromised application cannot cause much harm unless it interacts with the OS by making system calls
- Sequence of system calls executed is locally consistent during normal operation
- Some unusual sequence of system calls will be executed during exploitation
#### Accuracy 
Both signature-based IDS and Anomaly-based IDS are not 100% accurate in the following sense:
- If IDS raises an alarm, is it indeed an attack?
	- If not, this is called a false alarm or false positive
- If IDS does not raise an alarm, is it indeed benign?
	- If not, this is called a miss or false negative

Recall = $\frac{tp}{(tp+fn)}$, Precision=$\frac{tp}{(tp+fp)}$
#### Summary
Advantages
- Complements firewall
- Continues to improve
- Does not affect performance

Disadvantages
- High false alarm rate
- May miss some new attacks
- Requires security personnel to handle alarms and monitor track records
### Deployment of FW and IDS
- Firewall is always deployed at the perimeter of the protected facility (a network or a host)
	- It must have the capability of intercepting network traffic
	- Two firewalls create the DMZ for network servers facing internet traffic
- IDS is deployed side-by-side of the protected facility
# Software Security 
### Vulnerability
- Definition: a flaw in a software, firmware, or service component resulting from a weakness that can be exploited
- Potential consequences:
	- code injection: attacker manages to insert his own code to the victim program and run it
	- control flow hijacking: attacker changes the flow of the program by changing the data in use without modifying the victim code or injecting his own code
	- data leakage
	- execution correctness
	- denial of service
- The actual consequence depends on the program, the vulnerability, and how it is triggered
- An attack may involve multiple vulnerabilities
- **CVE**: Common Vulnerabilities and Exposures
#### Handling Program Input
Input refers to any source of data from outside the program and is not known when the code is written
	- data read through keyboard, mouse, file, network packets
	- command line arguments, environment variables
	- data supplied by other programs or configuration value by OS
#### Common Input Validation Vulnerabilities
- Malicious inputs can become code, or change the logic to do things that are not intended
- Common input validation vulnerabilities include:
	- OS command injection, directory traversal
	- Memory corruption vulnerabilities in C/C++
	- SQL injection, XSS
	- General insecure coding flaws that leak sensitive information
##### Command Injection (aka Shell Injection)
- Input validation that allows execution of arbitrary commands on the operating system
- The vulnerability occurs when the program uses user input data (such as command line arguments, form input data, cookies, HTTP headers, etc.) as (part of) a system shell
- To exploit this vulnerability, the attack typically involves the use of command-line specific special character ";"
##### Directory Traversal (aka Path Traversal)
- Input validation vulnerability that allows access of unauthorised files and directories, e.g. those that are stored outside the web root folder
- This vulnerability occurs when the program uses user input data, such as form input data, to access files/directories
- To exploit this vulnerability, the attack typically involves the use of the sequence of special characters (../) and it's variations (../../../)
### Buffer Overflow
A condition at an interface under which more input can be placed into a buffer or data holding area than the capacity allocated, overwriting other information. Attackers exploit such a condition to crash a system or to insert specially crafted code that allows them to gain control of the system
1. User enters data into a web form
2. Web form is sent to server
3. Server writes data to buffer, without checking length of the input data
4. Data overflows from buffer
5. Sometimes, overflow can enable an attack
#### Consequence of Buffer Overflow
- Overflow in buffer1 modifies data in buffer2. The direction of overflow is towards the higher addresses
- The consequence depends on how the modified data is used by the program
### Countermeasures for Memory Corruption Vulnerabilities
#### Good programming practices
- Use safe APIs instead of unsafe APIs 
	- use `strncpy` instead of `strcpy`
	- instead of using `Runtime.exec()` to issue a 'mail' command, use secure API from `javax.mail.*`
- Apply proper input validation
	- Identify and specify maximum expected size of input
	- Check for things that are not allowed (blacklist)
		- sanitise/escape blacklisted characters (e.g., ;)
		- blacklist may not be exhaustive
	- Check for things that are allowed (whitelist)
		- may cause false positives
#### System Supports
- Immutable code and inexecutable data in the memory
	- The OS has an ACL-like approach to specify whether bytes in a memory region can be read, written, or executed
	- An effective way to prevent an adversary from inserting its own code
- Address randomisation when a program is launched
	- It will be harder for the attacker to predict the consequence of overflow or choose the target to attack
	- Windows, Linux, and other UNIX variants by default has enabled coarse grained address space layout randomisation (ASLR)
- Control flow integrity enforcement
	- During execution, the program checks whether a control transfer destination in use violates predefined policies
	- supported by modern compilers, e.g. GCC, LLVM, or Microsoft Visual Studio
#### Language Support (Memory-Safe Languages)
- Some programming languages have built-in defence against memory errors: Java, C#, Python, Rust
- They are typically interpretation based exection 
### Malware
#### Categorisation
- Based on independence
	- Parasitic: fragments of programs that cannot exist independently of some actual programs
	- Self-contained: independent programs scheduled and run by OS
- Based on replication
	- Replicating: produce one or more copies of itself
	- Non-replicating: does not replicate
#### Worm
a program that can replicate itself and send copies from computer to computer across network connections
#### Botnet
Bot (a.k.a. zombie) is a program that secretly takes over an Internet-attached computer and uses that computer to launch attacks, under a remote control
- Remote Control Facility: 
	- by an IRC channel (Internet Relay Channel)
	- covert communication channels via protocols e.g., HTTP
- Botnet construction:
	- need a vulnerability in a large number of systems
- Widely used in DDoS attacks and Bitcoin mining
#### Malware Concealment
- **Encrypted virus**: a random encryption key is created. The decryption key is stored with the virus
- **Polymorphic virus**: A virus that mutates with every infection, making detection by the signature of the virus impossible
	- can be done by encryption, insert superfluous instructions or interchange the order of independent instructions
- **Metamorphic virus**: As with a polymorphic virus, it mutates with every infection. Differently, it rewrites itself completely at each iteration. Both the behaviour and appearance/signature can be changed
### Program Analysis
Program Analysis analyses and extracts program signatures and behaviours
- Two types of program analysis in general 
	- Static: does not execute program
	- Dynamic: executes program
- It can be used to extract malware signatures and understand their behaviours such as suspicious network activities
- Likewise, it can be used to analyse a given program to detect vulnerabilities based on known insecure coding signatures and known bad behaviours such as crashes
#### Static Analysis
- Does not need to execute the software
- Checks features such as file name, MD5 checksums or hashes, file type, file size
- Statically analyses its source code or binary code to understand its behaviour, typically by extracting graphs (CFG, call graph, etc.)
	- e.g. APIs used to access sensitive data
	- e.g. calling a network API immediately after accessing sensitive data is an indication of data leakage
- **Advantage**: rich semantics, low overhead, easy to implement, risk-free
- **Limitation**: easy to evade (obfuscation), false alarms
##### Control-Flow Graph (CFG)
- A way to represent the possible flow of control inside a function 
- Nodes: called basic blocks. Each block consists of straight-line code without jumps
- Edges: an edge A -> B means that the control could flow from A to B
- There is one unique entry node and one unique exit node
#### Dynamic Analysis 
- Monitor and control malware execution to collect the malware's runtime behaviour such as API calls, data flow, network traffic, etc. 
- **Advantage**: can obtain real data flows and control flows
- **Limitation**: difficult to extract semantic information, high overhead to securely monitor malware execution (since malware may attack the monitor)
	- Malware may also be checking whether it is being monitored
### Fuzz Testing - a form of dynamic analysis
- Automatically generate test cases
- Anomalous test cases are sent into a target interface
- Application is monitored for errors
- Inputs are generally either text based, file based, or network based
# Web Security
## Sessions
- HTTP is a stateless protocol
- For various business purposes, web applications tend to maintain states by establishing sessions
- Web applications can establish sessions (shared state) between participants and refer to this common state when authorising requests
- Sessions between client and server are established through session identifiers
### Session Identifiers
- Server creates a session identifier (SID) and transmits it to the client
	- Typical threat model at this layer: SID can be captured in an end system but not during transit
		- i.e., assume communication is secure, e.g. using SSL/TLS
- Server may authenticate a user before the SID is issued and encode this fact in the SID
- Server may issue SID without prior user authentication for checking that requests belong to a given session
- Client includes SID in subsequent requests to the server; requests are authenticated as belonging to a session if they contain the SID
### Transferring Session Identifiers 
- Cookie: sent by server in a Set-Cookie header field in the HTTP response; the browser stores cookie in `document.cookie` and includes it in requests with a domain matching cookie's origin
- Note: Session ID can also be included at the Business application layer - for example,
	- Request (GET/POST) parameter: SID stored in a hidden field in an HTML form
### Session Persistence
- Session can persist between login and logout
	- Closing a window does not necessarily close a session to that web site; you usually have to log out explicitly
- Session can persist for the duration of a business transaction
- Sessions can persist indefinitely
	- Raises privacy issues when user's surfing behaviour can be tracked over an extended period
## Session Attacks
- When sessions entail privileges, e.g. because a 'trusted' user has been authenticated or a session with a 'trusted' machine has been established, those privileges may be gained by session hijacking. 
	- Unpredictable session identifiers are preferable
- Flooding attacks send many requests for session establishment, exhausting resource at the receiver => to prevent this, network security f/w IDS
	- Example of denial-of-service attack
	- Stateless solutions are preferable
### Session Hijacking
- Attacker predicts a client's session id
- Attacker prepares a URL of the target host, with the predicted session id
- Attacker then sends request to the target server, with the URL
- Attacker is then authenticated to the server as the client, hijacking the client's session
### Cookie Poisoning
- Malicious client or outside attacker may modify a SID, e.g. to elevate their permissions when SIDs are used for access control
- Outsider may also try to guess a client's cookie, maybe after having contacted the server itself, and try to use the guessed cookie to impersonate the user (Session Hijacking)
- Cookie could also be 'stolen' from client or server
- Session identifiers must be unpredictable, and be stored in a safe place
- Server can prevent modification of SID by embedding a message authentication code (MAC) - is used for integrity proof - in the SID constructed from a secret only held at the server
### How to prevent Session Attacks?
- Session identifiers must be unpredictable
- must be stored in a safe place in both the client side and server side
- Server can prevent modification of SID by embedding a message authentication code (MAC) in the SID constructed from a secret only held at the server
## Same Origin Policy (SOP)
- for the sake of security, the browser must restrict JS execution with access control
- SOP is the basic security mechanism dictating that a document or script loaded from one origin cannot (directly) interact with a resource from another origin
	- It helps to isolate potentially malicious documents, reducing possible attack vectors
- SOP is enforced by all browsers
- Cross-origin accesses undergo the browser's permission checking
### Site Isolation (Chrome)
- Site Isolation ensures that pages from different websites are always put into different processes, each running in a sandbox that limits what the process is allowed to do
	- to leverage the underneath operating system to enforce process-based isolation
- It also makes it possible to block the process from receiving certain types of sensitive data from other sites
- As a result, a malicious website will find it much more difficult to steal data from other sites, even if it can break some of the rules in its own process. 
## Cross-Site Scripting (XSS)
- XSS attacks run a script in the browser that was not written by the web application owner
	- The vulnerability is some of the most common vulnerabilities in the internet
	- It is a special form of code injection
- In general, XSS can be classified into 
	- Stored XSS: the code is stored on the database prior to execution
	- Reflected XSS: the code is not stored but reflected by the server
	- DOM-based XSS: the code is stored and executed in the browser
### Stored XSS
- a.k.a. persistent XSS
- The form submitted by the attacker has the `<script>` tag. The form is interpreted as text, and is deposited to the database.
- However, the victim user views the data retrieved from the database. Her browser treats the tagged text as JavaScript code and executes i
- most common type of XSS attacks
- may affect the most users, depending on who views the data stored in the database
	- E.g., a comment posted in a web forum is visible to everyone in the internet
### Reflected XSS Vulnerability
- a.k.a. non-persistent XSS
- Potential Vulnerability: there could be a connection between the URL query parameters and objects in the result page
- Reflected XSS are those where the injected script is reflected off the web server, such as in an error message, search result, or any other response that includes some or all of the input sent to the server as part of the request
- The attacker sends the malicious URL to the victim user via email, web advertisement or other ways
- When the victim user clicks the URL, the server returns the HTML page which echoes back the query consisting of the JS code
- It is better at avoiding detection than stored XSS, but is harder to distribute to a wide number of users
	- can be launched at targeted users
### DOM-based XSS
- is an XSS attack (a.k.a "type-0 XSS") wherein the attack payload is execute as a result of modifying the DOM "environment" in the victim's browser used by the original client side script, so that the client side code runs in an "unexpected" manner
	- The page itself (i.e. the HTTP response) does not change, but the client side code contained in the page executes differently due to the malicious modifications that have occured in the DOM environment
- Both stored XSS and reflected XSS attacks require server-side flaws to inject malicious code. But DOM-based XSS does not have that requirement
#### Example
`insecure-bank.com/page.html#default=<script>alert(document.cookie)</script>`
- URI fragments (the part in the URI after the "#") is not sent to the server by the browser
- The web server only sees a request for page.html without any URI parameters
- The response from the server does **NOT** consist of malicious script which manifests itself at the client-side script at runtime
- A **flawed script** in the page accesses the DOM variable `document.location` and uses the parameter for default to create a new DOM object
### Defence against XSS
- Two fundamental defence strategies:
	- Filter server outputs / browser inputs: differentiate between HTML elements ('code') and user data
		- Clients can filter inputs 
		- Servers can sanitise outputs, escape, encode dangerous characters 
- Improve access control - XSS violates SOP (access control)
	- Authenticate origin (back to cryptography stuff)
	- Block execution of scripts in the browser altogether -> most secure but not practical
	- Authorise scripts explicitly (content security policy)
#### Solution 1: Filtering
- Trusted server, when constructing response page: HTML encoding of all data put into web page
	- e.g. markup delimiters <, >, ", & are encoded as &lt;, &qt; &quot;, &amp;
	- web server needs to tell the browser that `<script>` is NOT the JS code
- Trusted server, when sending the response page: filter for suspicious patterns
##### Limitations of Filtering
- Filtering is the current practice but...
- Only works well if you clear rules characterising good/bad inputs
	- Alternative: taint analysis; traces data flow through code from untrusted sources to trust sinks; raises alert if no sanitising operation is encountered
- Filtering is the current practice but...
	- Only works well if you have clear rules characterising good/bad inputs
		- Alternative: taint analysis; traces data flow through code from untrusted sources to trust sinks; raises alert if no sanitising operation is encountered
	- Has to be tailored to a specific scenario; has to deal with unspecified browser behaviour
	- Scattered code: input validation/output sanitisation not centrally enforceable
#### Solution 2: Improve Access Control
- Authenticate origin -> not really used in practice
	- Server could sign (PKI): client needs public verification key
	- Server could MAC to scripts; client needs secret key
- Browser, when rendering page from trusted server, checks that scripts are authorised by trusted server
	- Server could put authorised scripts in a specific directory and tell client about it (Content Security Policy)
### Blocking Script Execution & CSP
- Blocking all scripts seriously limits the web pages one can use today
- Block in-line scripts: Mozilla's Content Security Policy
	- All scripts for a page must be loaded from white-listed hosts
	- Scripts included via a `<script>` tag pointing to a white-listed host will treated as valid
	- All inline scripts, javascript: URIs, and event-handling HTML attributes will be ignored - `onload='alert();'`
- Server tells browser how to distinguish between it's own scripts and scripts injected into its web pages
# CSRF & SQL Injection
## Cross Site Request Forgery (CSRF)
- Parties involved: attacker, 'trusted', user, server
- Cross-site request forgery exploits 'trust' a target server has in a user to execute actions at the server with the user's privileges
	- Trust: user in some way authenticated at the server (cookie, authenticated SSL session, ...)
- Violate server's assumption about the end point of a request
- User had to follow a link to the server prepared by the attacker that contains a hidden request
	- Typically conducted using social engineering such as sending links via email or messages or in a page on a website
- For the application, as the user is authenticated, it is impossible to distinguish a legitimate request from a forged one
### Attack Pattern 
- User visits a page at attacker's site and clicks a link;
- Or user clicks on a link in email, social media, etc.
- When the user clicks the link (crafted by the attacker), the user's browser will send a request to the target server (pointed by the link)
- Server authenticates request as coming from user, because it comes from the user's browser
	- Actions (name and value pairs) in the request are executed by server with access rights of authenticated user
	- Session hijacking attack
### Defenses 
- Ultimate cause of attack: server only authenticates 'the last hop' of the entire request, but not the true origin of all its parts
- Defense: authenticates requests (actions) at the level of the web application ('above' the browser):
	- Check origin HTTP header
	- CSRFPreventionToken, e.g. HMAC
	- One time tokens
#### CSRF Prevention Tokens
- OWASP recommendation: Synchroniser Token Patern 
	- Server creates random "challenge" tokens associated with user session
	- Tokens inserted into HTML forms and links on all served pages
- Token value be reasonably fresh (e.g. generated once per session)
- Web application must validate each request by comparing received token to stored one
- Request without token or with wrong token are discarded
- Tokens must be unique, generator function must not expose patterns
#### Other CSRF Protections
- CAPTCHA 
	- Challenge-response test to ensure a request was made by a human being 
	- Imposes usability constraint
- Double Submit Cookies
	- Transmit tokens in two different ways, e.g. as HTTP header (cookie) and hidden form value
	- Works as long as attacker cannot circumvent SOP to read cookie information
### CSRF Protection from User's Perspective
- Log off web applications when not in use
- Avoid simultaneously browsing while logged into a sensitive application (e.g. banking, transaction applications)
- You do not want them to "remember me"
- Keep passwords securely 
## SQL Injection
- Gain access to the database by manipulating user inputs used in SQL queries
	- Inject special characters (syntactic meaning to SQL parser/interpreter) such as ' # OR ; =
- Can obtain sensitive information such as admin passwords for further exploitation of the system
- Can be used to delete database tables, upload files, create reverse shell, etc.
### Remark on SQL Injection
- Single quote ' is the string delimiter in SQL
- In a web application, a server-side script may construct SQL query as a string from query fragments and user input
- String passed to DBMS and executed as SQL query
- User input can now be interpreted as code by DBMS
- **Broken abstraction**: no clear distinction between data and code
### Defence against SQL Injection
1. Sanitise or validate user inputs so that dangerous inputs are made innocuous
	a. Filtering (blacklist or whitelist)
	b. Escaping - Replace dangerous characters with encodings - e.g. `'` -> `\'`
2. Bound parameters so that user inputs cannot be mistaken for code (clean solution to the problem)
- Additional precautions:
	- Avoid verbose error messages; error messages for invalid inputs can leak information about database, relations, names of columns, etc.
	- Least privilege: do not connect as sysadmin
