# From an open API doc to account takeover (LinkedIn post, 2026-10-25)

An open API doc is a map. Attackers don't need to guess your endpoints if you publish them.

On one engagement, unauthenticated Swagger/OpenAPI exposed ~190 endpoints. Alone, that's "informational". In a chain, it's where the critical findings started.

1. **Exposed API docs**: the docs list every route, parameter and role. Fix: require auth, or disable docs in production.
2. **Finding the sensitive routes**: password reset, profile, admin helpers are easy to spot when the docs name them. Fix: no security by obscurity, every route needs its own authorization.
3. **Broken object-level authorization (BOLA)**: an ID in the request is trusted without checking who owns the object. Fix: server-side ownership check on every object access.
4. **Weak reset / verification flow**: no rate limits or weak tokens turn data access into account control. Fix: rate limiting, single-use short-lived tokens, notify the user.

Result: account takeover. Score the chain, not the line item. Hide the map AND lock the doors. Retest after the fix.

Carousel version: [carousel.pdf](carousel.pdf)

`#APISecurity #AppSec #PenetrationTesting #BOLA #SecurityQA`
