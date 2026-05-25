# LLM Honeypot Prompt and Behaviour Rules

This file documents the commands used to inspect the prompt and behaviour rules used by the LLM-based honeypot. These rules controlled how the LLM was instructed to respond during simulated SSH terminal sessions.

## 1. Locating the Prompt Function

The following command was used to locate the prompt-building function inside `honeypot.py`:

```bash
grep -n "def build_prompt" honeypot.py
```

The prompt-building function was found in:

```text
honeypot.py
```

## 2. Inspecting Prompt and Behaviour References

The following command was used to search for prompt, system identity, Linux terminal, and honeypot behaviour references inside the Python files:

```bash
grep -nEi "prompt|system|instruction|behave|act|linux|terminal|shell|honeypot|realistic|respond|simulate|fake|role|assistant" honeypot.py ssh_honeypot.py
```

## 3. Inspecting the Prompt Section

The following command was used to inspect the section of `honeypot.py` where the LLM prompt and behaviour rules were defined:

```bash
sed -n '147,190p' honeypot.py
```

## 4. Prompt Purpose

The prompt was used to instruct the LLM to behave like a realistic Linux terminal during attacker interaction. It provided the LLM with system identity details, environment details, filesystem rules, and behaviour rules.

## 5. Confirmed System Identity Details

The prompt included system identity values such as:

```text
hostname
username
home directory
current directory
```

These values helped the LLM keep shell responses consistent during interaction.

## 6. Confirmed Environment Details

The prompt included simulated system environment details such as:

```text
Ubuntu 22.04.4 LTS
Linux kernel 5.15.0-91-generic
x86_64 architecture
eth0 network interface
IP address 10.10.70.10/24
default gateway 10.10.70.1
attacker IP 10.10.60.10
timezone Europe/Malta
current year 2026
```

## 7. Filesystem Rules

The prompt included filesystem rules to make the simulated environment behave more realistically.

Examples of confirmed filesystem rules included:

```text
Standard Linux files such as /etc/passwd, /etc/group, and /etc/hosts must exist.
Do not say core system files are missing.
User home directories exist under /home/.
The current user is defined by the prompt.
```

## 8. Behaviour Rules

The prompt included behaviour rules that controlled how the LLM should respond to commands.

Examples of confirmed behaviour rules included:

```text
Act like a normal bash shell.
If a command does not exist, return: bash: <cmd>: command not found
If a file does not exist, return: No such file or directory
If permission is denied, return: Permission denied
Prefer short, realistic Linux outputs.
Keep outputs consistent with previous responses.
Never invent different IP ranges.
Always use the defined IP address and network.
Keep time, users, and system details consistent across commands.
Never mention AI, models, or honeypots.
```

## 9. Purpose of Prompt and Behaviour Rules

These prompt and behaviour rules were used to make the LLM-based honeypot respond more like a real Linux SSH terminal. They helped improve realism, reduce inconsistent responses, and prevent the LLM from revealing that the environment was AI-generated or deceptive.
