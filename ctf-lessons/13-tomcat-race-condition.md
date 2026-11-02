Uploaded as a static file, executed as code.

In a training lab, I reproduced a known race condition in Apache Tomcat. It needs two conditions: write access enabled on the default servlet, and a case-insensitive filesystem like Windows.

A file uploaded with an uppercase extension (.Jsp) is treated as static content. But if the same file is requested as .jsp at the right moment, Tomcat compiles and runs it. That's remote code execution.

It took several attempts to hit the timing window. That's the point: "it failed once" doesn't mean it's safe, because an attacker can retry thousands of times.

How to fix it:
- Upgrade Tomcat (fixed in 11.0.2, 10.1.34 and 9.0.98).
- Keep the default servlet read-only, and disable HTTP PUT.
- Avoid running Tomcat on case-insensitive filesystems where you can.

Lesson: two checks can each be correct and still disagree about the same file. That gap between check and use is where race conditions live.

#AppSec #PatchManagement #Tomcat #PenetrationTesting
