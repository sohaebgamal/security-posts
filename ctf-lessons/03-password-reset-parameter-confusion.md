Same parameter, two values, and someone else's account.

In a training lab, a password reset form sent the same "email" parameter in two places: the URL and the request body.

The code used PHP's $_REQUEST, which merges both sources into one and picks a winner. Different parts of the flow ended up trusting different copies:

- The account lookup used the victim's email from the URL.
- The reset link went to the email in the body, which was mine.

The server found the right account and sent its reset link to the wrong person. No password cracking and no injection, just one request with two values.

This is why it's easy to miss: normal testing sends one value, and everything works. Automated scanners also tend to struggle with logic flaws like this one.

How to fix it:
- Read each input from one explicit source, such as $_POST, never a merged one.
- Send reset links only to the address stored for that account, never to one from the request.
- Add tests that send duplicate parameters in the URL and body.

Lesson: test what the code assumes, not only what the form allows. A browser sends one value, but an attacker's request doesn't have to.

Does your test plan include duplicate parameters?

#AppSec #WebSecurity #BusinessLogic #SecurityQA
