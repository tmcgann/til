To print the fingerprint of an SSH key:

```bash
$ ssh-keygen -lf ~/.ssh/id_rsa.pub
4096 SHA256:Fh24Sluy904KKf+43bvmSd82Mf8SBekj taylor@example.com (RSA)
```

If you want the old school md5 hash:

```bash
ssh-keygen -E md5 -lf ~/.ssh/id_rsa.pub
4096 MD5:11:22:33:44:55:66:77:88:99:00:aa:bb:cc:dd:ee:ff taylor@example.com (RSA)
```
