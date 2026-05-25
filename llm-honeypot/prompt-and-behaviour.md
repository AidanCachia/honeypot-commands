# LLM Honeypot Prompt and Behaviour Rules

This file documents the prompt and behaviour rules used by the LLM-based honeypot. These rules were defined inside `honeypot.py` and controlled how the LLM responded during simulated SSH terminal sessions.

## 1. Locating the Prompt Function

The following command was used to locate the prompt-building function inside `honeypot.py`:

```bash
grep -n "def build_prompt" honeypot.py
```

## 2. Inspecting Prompt and Behaviour References

The following command was used to search for prompt, system identity, Linux terminal, and honeypot behaviour references inside the Python files:

```bash
grep -nEi "prompt|system|instruction|behave|act|linux|terminal|shell|honeypot|realistic|respond|simulate|fake|role|assistant" honeypot.py ssh_honeypot.py
```

## 3. Inspecting the Prompt Section

The following command was used to inspect the section of `honeypot.py` where the LLM prompt and behaviour rules were defined:

```bash
sed -n '147,200p' honeypot.py
```

## 4. Prompt Purpose

The prompt was used to instruct the LLM to behave like a realistic Linux terminal during attacker interaction. It defined the simulated system identity, environment details, filesystem rules, behaviour rules, recent command history, and the command to execute.

## 5. Exact Prompt Rules

The following rules were taken from the prompt section in `honeypot.py`:

```text
- Never mention AI, models, or honeypots.

System identity:
hostname: {HOSTNAME}
username: {USER}
home: {HOME}
current directory: {cwd}

System environment:
- OS: Ubuntu 22.04.4 LTS
- Kernel: 5.15.0-91-generic
- Architecture: x86_64
- Interface: eth0
- IP address: 10.10.70.10/24
- Default gateway: 10.10.70.1
- Attacker IP: 10.10.60.10
- Timezone: Europe/Malta
- Current year: 2026

Filesystem rules:
- Standard Linux files such as /etc/passwd, /etc/group, /etc/hosts MUST exist.
- Do NOT say core system files are missing.
- User home directories exist under /home/.
- The current user is {USER}.

Behaviour rules:
- Act like a normal bash shell.
- If a command does not exist: bash: <cmd>: command not found
- If a file does not exist: No such file or directory
- If permission is denied: Permission denied
- Prefer short, realistic Linux outputs.
- Keep outputs consistent with previous responses.
- NEVER invent different IP ranges such as 10.0.2.x, 10.0.3.x, or 192.168.x.x.
- Always use the defined IP (10.10.70.10) and network (10.10.70.0/24).
- Keep time, users, and system details consistent across commands.

Recent command history:
{hist3}

Command to execute:
{cmd}
```

## 6. Purpose of Prompt and Behaviour Rules

These prompt and behaviour rules were used to make the LLM-based honeypot respond more like a real Linux SSH terminal. They helped improve realism, reduce inconsistent responses, and prevent the LLM from revealing that the environment was AI-generated or deceptive.
