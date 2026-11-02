One password, many users, zero lockouts.

In an Active Directory training lab, after building a list of valid usernames, I tried one common password against every account, staying under the lockout limit.

One account used it. It met the complexity policy (uppercase, number, symbol), and it's also in every password list. One guess per user was enough for a domain foothold.

Account lockout protects one account from many guesses. Spraying makes one guess against many accounts, so lockout never triggers.

How to fix it:
- Block common and breached passwords, not just weak patterns.
- Prefer long passphrases over complexity rules.
- Turn on MFA.
- Alert when many accounts fail from one source in a short time.

Lesson: "meets the policy" doesn't mean "hard to guess."

#ActiveDirectory #PasswordSecurity #BlueTeam #PenetrationTesting
