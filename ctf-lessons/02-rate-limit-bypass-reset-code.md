A rate limit that trusts the client isn't a rate limit.

In a training lab, a password reset flow looked well protected: a 4-digit code, a countdown, and a limit on attempts per IP.

The catch was how the server decided what "IP" meant. It read the X-Forwarded-For header, which the client controls.

So every few attempts, a new header value looked like a new visitor, and the counter started over. With only 10,000 possible codes, the rest was just a script. That ended in account takeover.

No single piece looks terrible on its own:
- A short reset code is weak but seems "protected" by the limit.
- The limit seems solid until you check where it gets its input.

Together, they remove the only thing standing between an attacker and the account.

How to fix it:
- Count attempts per account and per reset token, not only per IP.
- Trust X-Forwarded-For only when it's set by your own proxy.
- Use long, random, single-use reset tokens that expire quickly.
- Invalidate the token after a few failures, and notify the user.

Lesson: for every security control, ask "where does its input come from?" If the answer is the request, an attacker can probably change it.

How does your app count failed attempts?

#AppSec #WebSecurity #PenetrationTesting #SecurityTesting
