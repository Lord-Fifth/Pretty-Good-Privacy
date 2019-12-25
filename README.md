# Pretty-Good-Privacy

This guide shall introduce you to two core concepts

* **PGP** : Basic Guide can be found in this [Tutorial by The Privacy Guide](https://theprivacyguide.org/tutorials/pgp.html)
* **Web of Trust** : Core Concepts is explained in this [Tutorial by Linux.com](https://www.linux.com/tutorials/pgp-web-trust-core-concepts-behind-trusted-communication/) 
----

## Gnu PG Cheat Sheet
Cheat sheet to get started with PGP using GnuPG on GNU/Linux Machines.

### Install Gnu PG tool

```
sudo apt-get install gnupg
gpg --version

```

### Generate Keys

```
gpg --gen-key   //Generate Public and Private Key Pair

gpg --gen-revoke --armor --output=RevocationCertificate.asc <email.address>

gpg --list-secret-keys //list private keys

gpg --fingerprint <your_email>

```

**Last 8 Digits of fingerprint (without space) forms the  key_id**

### File Integrity Check using MD5 Checksum

```
touch file.txt
nano file.txt //Edit file
md5sum file.txt > checksum.md5 //Generate Checksum and export it to a file named checksum.md5
md5sum -c checksum.md5 //Check the integrity of file associated with generated checksum 
 
```

### File Integrity check with User Association using GPG

```
gpg --detach-sign test.txt //This will generate a file test.txt.sig
gpg --verify test.txt.sig  //Check the integrity, origin and authenticity of the file

```


## Encrypting files

### Upload Key to key server

```
gpg --keyserver pool.sks-keyservers.net --send-keys <your_key_id> 

```
**If the keyserver fails, try another which is a part of the [key server pool](https://sks-keyservers.net/status/)**

### Find and Import  Recipients Public Key

```
gpg --keyserver pool.sks-keyservers.net --search-keys <recipent_email_add>

```

### Encrypt a file using public key of recipient

```
gpg --encrypt --sign --armor -r <recipient_email> name_of_file

```

### Decrypt a file using private key

```
gpg file_name.asc //To be done at the recipients machine

```

### Exporting Private Key

```
gpg --armor --export-secret-keys <your_email> > <filename.asc>

```

----

## Web of Trust

### Sign Key

```
gpg --edit-key <key_id>

 >sign  
 >trust  
 >save

```

### Exported the Signed Key in Encrypted format 

```
gpg -a --export <key_id> | gpg -se -r <key_id> > <key_id>.asc.pgp

```

**Now Send the signed key file to its user via email/thumbdrive**


### On the receiver end

```
gpg --decrypt <key_id>.asc.pgp
gpg --import <key_id>.asc
gpg --keyserver pool.sks-keyservers.net --send-keys <key_id>  

```

----

## Other quick commands

### Revoke keys

```
gpg --import <revocation_cert.asc>
gpg --keyserver pool.sks-keyserver.net --send-keys <key_id>

```
### Refresh Keys 

``` 
gpg --keyserver pool.sks-keyservers.net --refresh-keys

``` 

**Do this once in a while to ensure that key has not been revoked by the user**

### List Signatures

``` 
gpg --list-sigs <key_id> 

``` 

### Shred Files

```
shred -n 200 -z -u  <file.name> // Always shread than rm for private files

```
**Take care in storing your keys safe**

In the event of a private key/key ring export to another memory media, shred the key files after the work is done 

### Exporting Private Key

```
gpg --armor --export-secret-keys <your_email> > <filename.asc> //Export Secret key to a file with .asc (ASCII) extension 

```

### Delete Keys

```
gpg --delete-keys <key-id>
gpg --delete-secret-key <key-id>  //delete Private Keys

```
