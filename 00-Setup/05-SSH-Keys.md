# SSH Keys

SSH (Secure Shell) is a secure network protocol used to connect to remote systems. SSH keys provide password less and secure authentication between your computer and remote servers or GitHub.

---

# Why SSH Keys?

- Secure authentication
- No need to enter passwords repeatedly
- Used for GitHub, Linux servers, and cloud services
- More secure than password based login

---

# Public Key vs Private Key

| Public Key | Private Key |
|------------|-------------|
| Shared with GitHub or servers | Kept secret on your computer |
| Used for authentication | Used to prove your identity |

> **Never share your private key.**

---

# Generate SSH Key

```bash
ssh-keygen -t ed25519 -C "your-email@example.com"
```

---

# View Public Key

```bash
cat ~/.ssh/id_ed25519.pub
```

Copy the output and add it to your GitHub account.

---

# Test GitHub Connection

```bash
ssh -T git@github.com
```

---

# Best Practices

- Use **ed25519** keys whenever possible.
- Never share your private key.
- Protect your private key with a passphrase.
- Add only the public key to GitHub or servers.

---

# Interview Questions
**Q: What is SSH?**  
**A:** SSH (Secure Shell) is a secure way to connect to another computer over a network.

**Q: Why are SSH keys used?**  
**A:** SSH keys let you log in securely without entering your password every time.

**Q: Difference between a public key and a private key?**  
**A:** The public key is shared with the server, while the private key stays secret on your computer.

**Q: How do you generate an SSH key?**  
**A:** Run the command:
```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

**Q: Why is SSH preferred over HTTPS for Git operations?**  
**A:** SSH is more secure and lets you push and pull code without entering your username and password every time.
