# 22110089_DangHoangViet_Lab2

# **Lab #2,22110089, Dang Hoang Viet, INSE331280E_02FIE**

# Task 1: Public-Key Based Authentication

**Question 1**

Implement public-key based authentication step-by-step with openssl according provided scheme. The mechanism involves the server sending an encrypted challenge to the client, which the client decrypts and signs, and the server then verifies the signature.

## 1. Generate Key Pair

### 1.1. Generate a private key for the client

Generate a private key for the client (2048-bit RSA) :

![image.png](image.png)

### 1.2. Extract Client's Public Key

Extract the public key from the client's private key:

![image.png](image%201.png)

## 2. Server Creates and Encrypts Challenge

### 2.1. Create a Challenge Message

Create a simple challenge message:

![image.png](image%202.png)

### 2.2. Encrypt the Challenge with Client's Public Key

Encrypt the challenge using the client's public key:

![image.png](image%203.png)

The file `encrypted_challenge.bin` is now the encrypted challenge that will be sent to the client.

## 3. Client Decrypts the Challenge

### 3.1. Decrypt the Challenge Using Client's Private Key

The client decrypts the challenge message with their private key:

![image.png](image%204.png)

## 4. Client Signs the Decrypted Challenge

### 4.1. Sign the Decrypted Challenge

The client signs the decrypted challenge using their private key:

![image.png](image%205.png)

The signed challenge is stored in `signed_challenge.bin`.

## 5. Server Verifies the Signature

### 5.1.  Verify the Signature Using Client's Public Key

The server verifies the signature to authenticate the client:

![image.png](image%206.png)

If the signature matches, OpenSSL will return a success message such as: 

![image.png](image%207.png)

This confirms:

1. The client successfully decrypted the challenge with their private key, proving ownership of the key pair.
2. The client correctly signed the challenge with their private key, demonstrating control of the private key.
3. The client's identity is verified since the signature can be validated with their public key.

# **Task 2: Encrypting large message**

Create a text file at least 56 bytes.

**Question 1**

Encrypt the file with aes-256 cipher in CFB and OFB modes.  Then, evaluate both cipher as far as error propagation and adjacent plaintext blocks are concerned. 

## 1. Prepare Files

### 1.1. Run Docker with OpenSSL

Run the following command to start an OpenSSL container with access to the shared folder:  

![image.png](image%208.png)

### 1.2. Create a Sample Text File

In `C:\openssl-demo`, create a file named `large_message.txt` with the following content:

![image.png](image%209.png)

## 2. Encrypting the File

### 2.1. Generate a Key and Initialization Vector (IV)

Generate a random 256-bit key (32 bytes) and a random 128-bit IV (16 bytes):

![image.png](image%2010.png)

### 2.2. Encrypt Using AES-256 in CFB Mode

Encrypt the file using AES-256 in **CFB mode**:

![image.png](image%2011.png)

### 2.3 Encrypt Using AES-256 in OFB Mode

Encrypt the file using AES-256 in **OFB mode**:

![image.png](image%2012.png)

### 2.4 Decrypt to Verify

To verify the encryption, decrypt the encrypted files and compare with the original file:

Decrypt CFB:

![image.png](image%2013.png)

Decrypt OFB:

![image.png](image%2014.png)

Check if the decrypted files match the original: