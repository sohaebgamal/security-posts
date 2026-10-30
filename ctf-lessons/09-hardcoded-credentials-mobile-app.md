If it ships in your mobile app, assume everyone has it.

In a training lab, I found an Android app on a compromised server. A decompiler (jadx) showed a config class holding a username and password, with the environment set to production.

Those weren't test values. They were valid Active Directory domain credentials.

That account then had rights over a group nested inside Domain Admins. So a secret in a mobile app became one of the final links in a chain that ended with control of the whole domain.

Why this keeps happening: compiled code feels hidden. It isn't. An APK can be unpacked and read with free tools, and obfuscation only slows that down.

How to fix it:
- Never put long-lived credentials in client apps.
- Use per-user login and short-lived tokens, issued by the server.
- Put a backend between the app and internal systems.
- Scan builds for secrets before release, and rotate anything that leaks.
- Review what rights each service account really needs, including nested groups.

Lesson: when you test a mobile app, decompile it first and look for secrets. Then ask what those secrets can reach, because that's the real impact.

Have you ever decompiled your own app?

#MobileSecurity #AppSec #ActiveDirectory #PenetrationTesting
