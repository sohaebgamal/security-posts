A Domain Admin logged in to a workstation once. That was enough.

In an Active Directory training lab, as local admin on a workstation, I pulled the credentials Windows keeps on the machine. Windows caches domain logons so people can sign in offline.

One cached entry had a weak password that cracked offline, and that account was a Domain Admin. With it, I could ask the domain controller to replicate everyone's password hashes (DCSync). One workstation became the whole domain.

How to fix it:
- Domain Admins never sign in to workstations. Use a tiered admin model and the Protected Users group.
- Give admin accounts strong, unique passwords.
- Lower the number of cached logons where offline sign-in isn't needed.
- Enable Credential Guard and LAPS.
- Alert on directory replication requests from machines that aren't domain controllers.

Lesson: where an admin signs in matters as much as how strong their password is.

#ActiveDirectory #CredentialAccess #BlueTeam #PenetrationTesting
