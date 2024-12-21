# OPENSSL Configuration 

## Overview 
OpenSSL is the world’s most widely used implementation of the Transport Layer Security (TLS) protocol. At the core, it’s also a robust and a high-performing cryptographic library with support for a wide range of cryptographic primitives.

OpenSSL is a de facto standard in this space and comes with a long history. 
Today, OpenSSL is ubiquitous on the server side and in many client programs. 
The command-line tools are also the most common choice for key and certificate management. 

![Configuration Steps Diagram](https://github.com/alsaeedi2007/OpenSSL/blob/main/Certificate%20Steps%20.png)


## Installing OPENSSL 
To install OPENSSL package in your linux Machine ( Debian based - like Ubuntu ) execute the below command

```
sudo apt install openssl -y
```
you can see the below screenshot taken while installing OPENSSL in Linux mint machine

![installing OPENSSL package](https://github.com/alsaeedi2007/OpenSSL/blob/main/openssl%20installation.png)
## Determine OpenSSL Version and Configuration

```
openssl version 
OpenSSL 3.0.13 30 Jan 2024 (Library: OpenSSL 3.0.13 30 Jan 2024)`
```
Refer to the below picture to check the OPENSSL version 

![OPENSSL version](https://github.com/alsaeedi2007/OpenSSL/blob/main/openssl%20version.png)

Now OPENSSL installed successfully and you can start using it

## private key generation 
First step tworad using OPENSSL is to generate private key and below the recommended points in generating privatekey for your machine.

- Private key should be extremely secure
- private key should not leave the machine that is generated from
- It is recommended to protect a private key with passpharse, so if lost at least they never get benefit from it since they dont know the passphrase
- passphrase should not be stored in a file in a system, should be memorized for security purposes
- if stored in a file then do not keep both encryption password and passphrase the same.
- use a strong encryption algorithem for the private key
- balance between long private key length and security ( Don't make it long as well as, try to make it acceptable ) 

to generate a private key, execute the below command:

```
openssl genrsa -aes256 -out myprivatekey.pem 4096

```
> [!tip] 
the number 4096 indicate the number of bit used in private key 
you can see the following picture below 

![Generating Private key ](https://github.com/alsaeedi2007/OpenSSL/blob/main/openssl%20genrsa.png)

to not be confused you can type the passphrase in a terminal by using the following command 
```
echo "T3st@123$" | openssl genrsa -aes256 -passout stdin -out myprivatekey3.pem 4096
```
you can see the screenshot taken from the machine

![echoing passphrase on terminal](https://github.com/alsaeedi2007/OpenSSL/blob/main/openssl%20passout%20example.png)

you can also stor the passphrase in a file and encrypt that file and use the encrypted file in openssl genrsa command, below is the illustration of that

**Creating a text file that contain the passphrase in a plain text** 
```
echo "T3st@123$" > mypassphrase.txt
```
**Encrypt the plain text passphrase**
```
openssl enc -aes-256-cbc -in mypassphrase.txt -out mypassphrase.enc
```

**My Recommendation** 
- Use the command: ``` echo "T3st@123$" | openssl genrsa -aes256 -passout stdin -out myprivatekey3.pem 4096 ```
- use the command : ``` openssl genrsa -aes256 -passout pass:T3st@123$ -out myprivatekey3.pem 4096 ```
- provide password interactively while excuting the command ``` openssl genrsa -aes256 -out myprivatekey3.pem 4096 ```, once you execute the command you will be prompted to give a passphrase and to confirm it again.

  






  

 

## Viewing Private key information 

to view the information of the private key you can use ``` openssl rsa -in myprivatekey3.pem ```, once you execute this command, the private key will be displayed in an encoded form as shown on the screenshot below 

![show private key info](https://github.com/alsaeedi2007/OpenSSL/blob/main/opessl%20rsa%2001.png)


## save the output to file 

``` openssl rsa -in myprivatekey3.pem -out myprivatekeyinfo ``` , you can see the output of the command in the below screenshot 

![openssl rsa info](https://github.com/alsaeedi2007/OpenSSL/blob/main/openssl%20rsa%2002.png) 



### Viewing private key paramaters 

you can view the privatekey paramaters and for that you have multiple options, like you can view the private key in a text format, see the below picture for more illustration 

command to be executed to view the paramaters of the private key 
```
openssl rsa -in myprivatekey.pem
```

 
![openss rsa text](https://github.com/alsaeedi2007/OpenSSL/blob/main/openssl%20rsa%2009.png)

#### Modulus Info 


to view the modulus information of the private key execute the below command:  

```
openssl rsa -in myprivatekey.pem -modulus -noout 
```


## Generating root certificate from private key 
the below diagram shows how to generate root certificate from private key 

![root certificate creation](https://github.com/alsaeedi2007/OpenSSL/blob/main/root%20certificate%2004.png) 

![root certificate creation step 02](https://github.com/alsaeedi2007/OpenSSL/blob/main/root%20certificate%2005.png)










