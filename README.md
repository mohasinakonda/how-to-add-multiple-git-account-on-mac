## Multiple Git Account on Mac

```bash
# Generate a new SSH key for your personal email
ssh-keygen -t ed25519 -C "your_personal_email@example.com" -f ~/.ssh/id_ed25519_personal -N ""

# Generate a new SSH key for your work email
ssh-keygen -t ed25519 -C "your_work_email@example.com" -f ~/.ssh/id_ed25519_work -N ""

```

step 2: Add the SSH keys to the ssh-agent

```bash
# Start the ssh-agent in the background
eval "$(ssh-agent -s)"
```

Step 3: Add your SSH private keys to the ssh-agent

```bash
ssh-add ~/.ssh/id_ed25519_personal
ssh-add ~/.ssh/id_ed25519_work
```

Step 4: Create or modify the SSH config file

```bash
nano ~/.ssh/config
```

Step 5: Add the following configuration to the SSH config file

```bash
# Personal GitHub
Host github.com-personal
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519_personal

# Work GitHub
Host github.com-work
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519_work
```

Step 6: Add Public Keys to GitHub

- get the public keys

```bash
cat ~/.ssh/id_ed25519_personal.pub
cat ~/.ssh/id_ed25519_work.pub
```

- Add the public keys to your GitHub account
- Go to Settings > SSH and GPG keys > New SSH key
- Paste the public key and click Add SSH key

Step 7: Test the SSH connection

```bash
ssh -T git@github.com-personal
```

Finally got success message

```bash
Hi your_personal_email! You've successfully authenticated, but GitHub does not provide shell access.
```
