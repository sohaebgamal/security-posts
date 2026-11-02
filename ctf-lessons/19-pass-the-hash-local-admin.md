One local admin password, reused on every machine, turns one compromised machine into many.

In an Active Directory training lab, I took the local administrator's password hash from one workstation and tried it on other machines. It worked on a server too. With Pass-the-Hash, there's no need to crack anything: the hash itself logs you in.

On that server, a Domain Admin's credentials had been left behind, and that led to the domain controller. The DC was behind a firewall, but a tunnel through one host that could see both networks reached it anyway.

How to fix it:
- Use LAPS so every machine has a unique, rotating local admin password.
- Block network logons for local accounts.
- Never leave privileged credentials on member servers.
- Don't rely on segmentation alone, and watch for unusual NTLM logons between machines.

Lesson: in Windows, the hash is the password.

#ActiveDirectory #LateralMovement #WindowsSecurity #BlueTeam
