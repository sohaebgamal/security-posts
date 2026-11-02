A password manager is only as strong as its master password.

In a training lab, after getting a shell on a monitoring server, I found a readable config file with a service account's password. The same password also worked for SSH as a real user.

In that user's backup folder was a KeePass database. Its master password was a single dictionary word, and a common wordlist cracked it. Inside was the root password.

Once a vault file is copied, guessing happens offline. There's no lockout and no rate limit, so the master password is the only defense.

How to fix it:
- Use a long, random passphrase for every vault, plus a key file or hardware key if supported.
- Never reuse a service account password for an interactive login.
- Restrict who can read config files and backups.
- Don't store the root password where a web compromise can reach it.

Lesson: protect the "keys to everything" like they're the target, because they are.

#PasswordSecurity #CyberSecurity #LinuxSecurity #PenetrationTesting
