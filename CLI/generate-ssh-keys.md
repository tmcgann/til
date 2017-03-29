I had to generate an SSH key for the _xth_ time so I thought I'd document the basic command for future reference.

```
ssh-keygen -d rsa -b 4096 <keyname>
```

Don't bother copying the public key to a remote server manually. `ssh-copy-id` FTW!

```
ssh-copy-id -i <keyname> <user>@<server>
```
