Deleting a password in a new commit doesn't delete it.

In an Active Directory training lab, an internal Git server hosted a readable repo. The latest commit said "remove hardcoded credentials", and the config file was clean.

The commit before it still had everything: a service account password that worked on the domain, an app secret key, and the default password given to new users. The build logs also printed that default password.

How to fix it:
- Once a secret is committed, treat it as leaked and rotate it first. Cleaning history comes second.
- Keep secrets in a secrets manager, not in the repo.
- Add secret scanning before commit and in CI (for example gitleaks or trufflehog).
- Never print secrets in build logs.
- Don't give every new account the same default password.

Lesson: when you review a repo, read the history, not just the latest version. A commit message like "remove secrets" points straight at them.

#DevSecOps #SecretsManagement #ActiveDirectory #AppSec
