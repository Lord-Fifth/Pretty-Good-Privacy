# Pretty-Good-Privacy

## Gnu PG Cheat Sheet

### Install Gnu PG tool

```
sudo apt-get install gnupg

```

### Generate Keys

```
gpg --gen-key   //Generate Public and Private Key Pair

gpg --gen-revoke --armor --output=RevocationCertificate.asc <email.address>

gpg --list-secret-keys //list private keys

gpg --fingerprint <your_email>

```

### File Sharing using MD5

```
touch file.txt
nano file.txt
md5sum file.txt > checksum.md5
md5sum -c checksum.md5
 
```

### GPG Way to create user association

```
gpg --detach-sign test.txt
gpg --verify test.txt.sig

```


## Encrypting files

### Find Keys

```
gpg --keyserver pool.sks-keyservers.net --send-keys <email_id>

gpg --keyserver pool.sks-keyservers.net --search-keys <email_add>

```

### Encrypt

```
gpg --encrypt --sign --armor -r <recipient_email> name_of_file

```

### Decrypt

```
gpg file_name.asc

```


### Exporting Private Key

```
gpg --armor --export-secret-keys <your_email> > <filename.asc>

```

## Sign Keys

```
gpg --edit-key <key_id>

 >sign
 >trust
 >save

```


### Send Signed Keys

```
gpg -a --export <key_id> | gpg -se -r <key_id> > <key_id>.asc.pgp

```

Now Send the pgp file via email/thumbdrive

### What the other user should do

```
gpg --decrypt <key_id>.asc.pgp
gpg --import <key_id>.asc
gpg --keyserver pool.sks-keyservers.net --send-keys <email_id>  

```

### Worst_Case

```
gpg --keyserver pool.sks-keyservers.net --send-keys <email_id_or_key_id>

```

### Refresh Keys

```
gpg --keyserver pool.sks-keyservers.net --refresh-keys

```

### List Signatures

```
gpg --list-sigs <key_id>

```

### Shred Files

```
shred -n 200 -z -u  <file.name>

```

### Delete Keys

```
gpg --delete-keys <key-id>
gpg --delete-secret-key <key-id>

```
