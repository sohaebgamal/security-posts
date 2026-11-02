The path check worked. The secret was inside the allowed path.

In a training lab, a file viewer read files by a path the user supplied. The developer had added two restrictions: only local files, and only inside the web root. That really did stop me from reading system files.

But the config file holding an HR account's password lived inside the web root. The restriction protected everything except the one file that mattered.

With that password I logged in, and reading the app's own source through the same viewer showed a SQL injection in the search box. That led to the admin account.

How to fix it:
- Don't let users choose file paths. Map an ID to a fixed list of files.
- Keep config files and secrets outside the web root, in environment variables or a secrets manager.
- Use prepared statements for every query.
- Turn off detailed error messages in production.

Lesson: an allowlist is only as safe as what's inside it. Before trusting a folder restriction, ask which sensitive files already live in that folder.

#AppSec #WebSecurity #SecureCoding #PenetrationTesting
