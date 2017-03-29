I had to generate an SSH key for the xth time so I thought I'd document the steps.

```
ssh-keygen -d rsa -b 4096 <filename>
```

Don't bother copying the key manually. `ssh-copy-id` FTW!

```
ssh-copy-id -i <filename> <user>@<server>
```
