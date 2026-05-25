# LLM Honeypot Dataset Files

This file documents the dataset-related commands used for the LLM-based honeypot. These commands were used to access, inspect, and edit the dataset files that supported the simulated Linux environment and command response behaviour.

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

## 5. Attack Patterns Dataset

The `attack_patterns.json` file stored groups of attacker-style commands used to classify or recognise common attacker behaviour.

Examples of command categories included:

```text
filesystem_discovery
persistence_attempts
download_tools
```

## 6. Corrections Dataset

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

## 7. Editing Dataset Files

The following command was used to edit the simulated filesystem dataset:

```bash
nano ~/llmhoneypot_v2/dataset/filesystem.json
```

The following command was used to edit the attack patterns dataset:

```bash
nano ~/llmhoneypot_v2/dataset/attack_patterns.json
```

## 8. Recreating the Simulated Filesystem Dataset

The following command was used to overwrite or recreate the simulated filesystem dataset using terminal input:

```bash
cat > ~/llmhoneypot_v2/dataset/filesystem.json <<'EOF'
```

## 9. Purpose of Dataset Files

These dataset files supported the LLM-based honeypot by providing structured information used to simulate a Linux environment and improve response consistency. The files helped define fake directories, fake file contents, protected files, attacker command patterns, and corrected responses for selected Linux commands.
