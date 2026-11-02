A feature that fetches a URL for you can fetch your cloud keys too.

In a training lab that simulated AWS, a web app downloaded images from any URL the user gave it. The request came from the server, so it could reach places the user can't, including the instance metadata service.

The metadata service returned temporary credentials for the app's cloud role. That role could read a production secrets bucket it never needed.

The chain: SSRF → metadata service without a token → role credentials → a role with too much access.

How to fix it:
- Allowlist the domains the app may fetch, and block internal and link-local addresses.
- Require IMDSv2 with a hop limit of 1.
- Give each role only what it needs: a web role shouldn't read production secrets.
- Don't leave storage buckets open to anonymous reads.

Lesson: the impact of SSRF is what the server can reach, plus what its identity is allowed to do.

#CloudSecurity #AWS #SSRF #AppSec
