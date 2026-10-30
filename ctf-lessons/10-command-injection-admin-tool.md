"It's admin-only" isn't a security control.

In a training lab, an admin panel had a small maintenance tool: enter a host and it pings it. The code looked roughly like this:

shell_exec("ping -c 1 $host");

The input goes straight into a shell, so the shell treats anything extra as another command. Separators like ; and | worked, which meant running commands on the server. That's OS command injection (CWE-78).

The usual reaction is "only admins can reach that page." But in this lab, a separate SQL injection bypassed the login, so the attacker was already an admin. One flaw opened the door to the next.

How to fix it:
- Avoid the shell. Use a native library or an exec call that takes arguments as an array.
- Validate the host against a strict IP or hostname pattern.
- Run the web service with the least privileges possible.
- Review internal and admin tools with the same care as public features.

Lesson: an authentication check reduces who can reach a bug, but it doesn't remove the bug. Small "diagnostic" features deserve a close look, because they're often written quickly and rarely reviewed.

What's the oldest admin tool still running in your app?

#AppSec #WebSecurity #CommandInjection #SecurityQA
