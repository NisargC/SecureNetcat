## Application Overview

Versions -

OS: Ubuntu 14.04.6 LTS<br>
Python: 3.4.3

Secure netcat is a simple tool which is an implementation of netcat with confidentiality and integrity.
The application can be used as secure tool for file sharing or messaging over the linux terminal.

1.	The communication over TCP sockets uses AES-256 along with HMAC to give a secure form of netcat. The input can be piped-in to the client and the output can be piped-out at server. 
2.	Used Galois/Counter Mode (GCM) to combine AES with HMAC to give an encrypt-then-MAC Authentication encryption.
3.	PBKDF2 (Password-Based Key Derivation Function 2) is used for key derivation to reduce vulnerabilities to brute force attacks.
4.	We are using the Pycryptodome library to get access to these tools (AES, GCM, PBKDF2)
5.	Two way pipe between client and server implemented using select statement. This means that once the client is connected to the server, any input to STDIN of server will be securely transmitted to client's STDOUT and input to client's STDIN will go to STDOUT of the server.
6.	Message objects are encrypted and converted to JSON before being transmitted over the network.

## How to Run

#### File sharing mode

##### Client
```
./snc --key <KeyForAESEncrpytion> <Server IP> <Server port> < <Input File> > <Output File>
```
##### Server
```
./snc --key <KeyForAESEncrpytion> -l <Server Port> > <Output File> < <Input File>
```

#### Messaging mode

##### Client
```
./snc --key <KeyForAESEncrpytion> <Server IP> <Server port>
```
##### Server
```
./snc --key <KeyForAESEncrpytion> -l <Server Port>
```
Type in the messages and hit Ctrl+C to exit.