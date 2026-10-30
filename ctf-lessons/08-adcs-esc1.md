One certificate template can let a low-privileged user log in as someone else.

In a training Active Directory lab, I started with a password someone had left in a user's description field. It got me a normal domain account with nothing special about it.

Then I checked Active Directory Certificate Services and found the misconfiguration known as ESC1. A template is dangerous when these conditions come together:

- Enrollee Supplies Subject: the requester chooses who the certificate is for.
- Client Authentication: the certificate can be used to log in.
- Enrollment open to Authenticated Users, with no manager approval.

So a normal user can request a certificate in another user's name, and the domain accepts it as proof of identity.

What makes this worse: changing that user's password doesn't help, because the certificate is not based on the password.

How to fix it:
- Turn off Enrollee Supplies Subject on authentication templates, or require manager approval.
- Limit enrollment to the groups that need it.
- Audit templates regularly with tools like Certipy or BloodHound.
- Remove passwords from AD attributes, and rotate any you find.

Lesson: AD CS is often set up once and then forgotten. When did your team last review it?

#ActiveDirectory #ADCS #RedTeam #PenetrationTesting
