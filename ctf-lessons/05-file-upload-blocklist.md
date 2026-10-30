The upload form blocked .php. The server still ran PHP.

In a training lab, a file upload page rejected .php files, and that looked like the job was done.

But Apache can be configured to treat other extensions as PHP too, such as .phtml. The form was checking a list of forbidden names, while the server was deciding what to execute by its own rules. Those two lists didn't match.

The uploaded file landed in a public folder where the server would execute it, and that gave remote code execution.

Three weaknesses lined up:
- A blocklist, which only stops what its author thought of.
- Uploads stored inside the web root.
- A folder allowed to execute scripts.

Fixing any one of them would have broken the chain.

How to fix it:
- Use an allowlist of the exact extensions you need.
- Generate a random file name on the server, and ignore the user's.
- Store uploads outside the web root, or disable script execution in that folder.
- Check the real file content on the server. Don't trust the extension, the Content-Type, or the first few bytes.

Lesson: ask what the server will do with the file after upload, not only whether the form accepts it.

Can a file uploaded to your app ever be executed?

#AppSec #WebSecurity #FileUpload #PenetrationTesting
