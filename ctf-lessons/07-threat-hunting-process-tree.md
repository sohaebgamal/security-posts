The ransomware note tells you how the attack ended. The process tree tells you how it started.

In a threat hunting lab, the scenario began with encrypted machines. Working backwards through the logs, the first step turned out to be ordinary: a user downloaded what looked like a 7-Zip installer.

The chain looked like this:

browser → msiexec → temporary installer process → PowerShell downloading a script → a new service running as SYSTEM

Every step can look normal alone. People install software, and admins use PowerShell. The parent-child relationship is what gives it away: why would an installer launch PowerShell to fetch a remote script?

For each suspicious event, I asked four questions:
- Who ran it? (user)
- What exactly ran? (full command line)
- Where? (host)
- What started it? (parent process)

The detection isn't about the vulnerability. It's about making this visible:
- Collect process creation logs with full command lines.
- Alert on installers spawning script engines.
- Alert on PowerShell download patterns and on new services.
- Restrict software installs to approved sources.

Lesson: don't hunt single events, hunt relationships. A single log line is a clue, and the chain is the story.

Could your logs rebuild a chain like this today?

#ThreatHunting #SOC #BlueTeam #IncidentResponse
