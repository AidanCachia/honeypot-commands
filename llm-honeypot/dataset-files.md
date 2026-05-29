# LLM Honeypot Dataset Files

This file documents the dataset-related commands used for the LLM-based honeypot. These commands were used to access and inspect the dataset files that supported the simulated Linux environment and command response behaviour.

## 1. Accessing the Dataset Folder

The following command was used to enter the dataset folder:

```bash
cd ~/llmhoneypot_v2/dataset
```

## 2. Listing Dataset Files

The following command was used to list the dataset folder contents:

```bash
ls
```

The dataset folder contained the following files:

```text
attack_patterns.json
corrections.json
filesystem.json
llm_usage_attacker5.log
```

## 3. Inspecting All Dataset Files

The following command was used to list the dataset folder and inspect the main JSON dataset files:

```bash
cd ~/llmhoneypot_v2/dataset && \
echo "===== DATASET FILES =====" && ls -lh && \
echo "\n===== filesystem.json =====" && cat filesystem.json && \
echo "\n===== attack_patterns.json =====" && cat attack_patterns.json && \
echo "\n===== corrections.json =====" && cat corrections.json
```

## 4. Simulated Filesystem Dataset

The `filesystem.json` file defined fake Linux directories, fake file contents, and protected files used by the LLM honeypot.

Examples of simulated directories included:

```text
/
/etc
/home
/home/llmhoneypot
/home/llmhoneypot/.ssh
/home/llmhoneypot/Documents
/var/log
/var/www/html
/proc
```

Examples of simulated files included:

```text
/etc/passwd
/etc/hosts
/home/llmhoneypot/Documents/notes.txt
/home/llmhoneypot/.ssh/authorized_keys
/var/log/auth.log
/var/www/html/index.html
/proc/cpuinfo
```

The file also included protected files such as:

```text
/etc/shadow
```

## 5. Simulated SSH Files

The LLM honeypot simulated SSH-related files through the `filesystem.json` dataset file. This included a fake `.ssh` directory and an `authorized_keys` entry.

The following command was used to confirm the simulated SSH entries inside `filesystem.json`:

```bash
grep -n ".ssh" ~/llmhoneypot_v2/dataset/filesystem.json
```

The confirmed simulated SSH entries included:

```text
/home/llmhoneypot/.ssh
/home/llmhoneypot/.ssh/authorized_keys
```

The actual SSH host key used by the Paramiko-based SSH server was stored in the LLM honeypot project folder:

```text
/home/llmhoneypot/llmhoneypot_v2/host_rsa.key
```

The following command was used to confirm the host key file:

```bash
ls -lh ~/llmhoneypot_v2/host_rsa.key
```

## 6. Attack Patterns Dataset

The `attack_patterns.json` file contained grouped attacker-style command patterns used by the LLM honeypot dataset. These categories helped represent common attacker behaviours such as filesystem discovery, network reconnaissance, privilege escalation, persistence attempts, and download tool usage.

Examples of command categories included:

```text
filesystem_discovery
network_recon
privilege_escalation
persistence_attempts
download_tools
```

Examples of commands stored within these categories included:

```text
cat /etc/passwd
ifconfig
ip route
sudo -l
wget
curl
nc
```

## 7. Corrections Dataset

The following command was used to view the beginning of the corrections dataset:

```bash
head -n 50 corrections.json
```

The `corrections.json` file stored corrected outputs for selected Linux commands, helping the LLM honeypot return more consistent responses.

Examples of corrected commands included:

```text
cat /etc/group
cat /etc/os-release
hostnamectl
```

## 8. Purpose of Dataset Files

These dataset files supported the LLM-based honeypot by providing structured information used to simulate parts of a Linux environment and improve command-response consistency. The files contained simulated directories, fake file contents, protected file entries, attacker-style command patterns, corrected responses for selected Linux commands, and simulated SSH-related entries.
