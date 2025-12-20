#Learnings are stored here

Store the technical know hows of the studysSSH known hosts


This is how you write **Linux commands, YAML, Python, Go**, etc.

---

## Step 7: Full example (COPY THIS)

Paste this into `ssh-known-hosts.md`:

```md
# SSH known_hosts

## What is it?
`known_hosts` is a file used by SSH to store server fingerprints.

## Why is it needed?
- Prevents man-in-the-middle attacks
- Ensures you connect to the same server
- Protects against fake servers

## Common commands
```bash
ssh user@server
ssh-keygen -R hostname

