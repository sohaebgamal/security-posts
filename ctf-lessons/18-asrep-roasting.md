One checkbox in Active Directory hands out crackable password hashes.

The setting is "Do not require Kerberos preauthentication." With it enabled, anyone can ask the domain controller for a response for that user, and part of that response is encrypted with a key based on the user's password. It can be cracked offline, with no lockout and no failed logins in the logs.

In the lab, one account had this setting. Its password was a simple keyboard pattern and cracked instantly with a common wordlist. Any normal domain user can query AD to find accounts like this.

How to fix it:
- Find accounts with this setting and turn it off.
- If an account truly needs it, give it a long random password.
- Watch for Kerberos ticket requests without pre-authentication (event 4768).
- Audit account settings regularly.

Lesson: a legacy setting plus a weak password is an attack that makes almost no noise.

#ActiveDirectory #Kerberos #RedTeam #BlueTeam
