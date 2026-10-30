The account had no sudo rights, and it was still effectively root.

In a training lab, I logged in as a normal user, and my first command was id.

One group stood out: lxd.

It doesn't look dangerous, but membership in that group lets a user create privileged containers and mount the host's filesystem inside them. Root inside that container can read and change the host's files. No kernel exploit, no SUID hunting, and no sudo needed. The system was working as designed.

The docker group has the same problem. Both are often added for convenience: "the developer just needs to run containers."

How to fix it:
- Treat lxd and docker group membership as equal to root access.
- Audit these groups regularly, and remove anyone who doesn't need them.
- Use rootless containers where you can.
- Alert on new group members and on privileged containers that mount the host filesystem.

Lesson: privilege isn't only sudo. Before calling an account "low privilege," check what its groups can actually do.

Who's in the docker group on your servers right now?

#LinuxSecurity #PrivilegeEscalation #ContainerSecurity #PenetrationTesting
