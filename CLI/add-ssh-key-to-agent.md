Start the ssh-agent in the background.

```bash
eval "$(ssh-agent -s)"
```

Add ssh private key to ssh-agent

```bash
ssh-add ~/.ssh/id_rsa
```

List ssh keys added to ssh-agent.

```bash
ssh-add -l
```
