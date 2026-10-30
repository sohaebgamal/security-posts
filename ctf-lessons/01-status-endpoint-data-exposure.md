A "harmless" status endpoint gave me the map to an industrial plant's controls.

In a training lab, the login page held up. SQL injection and auth bypass went nowhere, and brute force didn't get me in.

The real problem was a status API the dashboard called every few seconds.

It was two flaws working together:

1. Missing access control and excessive data exposure
The API needed no login and returned far more than the page displayed: an internal secret, a server path, and which registers control pressure and valves.

2. An industrial protocol with no authentication
Classic Modbus TCP has no login. Anyone who can reach the port can read and write process values.

One write raised the pressure value, another disabled cooling, and nothing stopped that combination. In the lab, that meant a simulated blow-out.

How to fix it:
- Require authentication on status and monitoring endpoints too.
- Return only the fields the client needs, and never secrets.
- Separate IT from OT networks, and limit who can reach Modbus.
- Enforce safety limits with interlocks a network write can't override.

Lesson: when you test an API, read the raw response, not just the screen. The risk is often in the fields nobody displays.

When did you last check what your "read-only" endpoints return?

#CyberSecurity #APISecurity #ICSSecurity #PenetrationTesting
