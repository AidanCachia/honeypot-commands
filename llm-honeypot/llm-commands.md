# LLM-Based Honeypot Commands

This file documents LLM-based SSH honeypot commands that were found in the LLM honeypot VM command history. These commands relate to checking the project folder, running the Python honeypot, checking port `2222`, checking Ollama, and inspecting honeypot logs.

The purpose of this file is to document verified commands used during the project. It does not claim to be a full fresh installation guide from scratch.

## 1. Accessing the LLM Honeypot Folder

The following command was used to enter the LLM honeypot project folder:

```bash
cd ~/llmhoneypot_v2
```

## 2. Listing Project Files

The following command was used to list the files inside the LLM honeypot folder:

```bash
ls
```

## 3. Checking LLM Honeypot Script Configuration

The following command was used to check important configuration values inside `ssh_honeypot.py`, including the host, port, authentication logic, Ollama-related references, and Paramiko usage:

```bash
grep -nEi "VALID_USERS|username|password|PORT|HOST|MODEL|ollama|generate|chat|paramiko" ~/llmhoneypot_v2/ssh_honeypot.py
```

## 4. Running the LLM Honeypot Script

The following command was used to run the LLM honeypot script directly:

```bash
python3 ssh_honeypot.py
```

The following commands were used to run the honeypot in the background and save output into run log files:

```bash
nohup python3 ssh_honeypot.py > honeypot_run.log 2>&1 &
```

## 5. Checking Whether the LLM Honeypot Was Running

The following commands were used to check whether the LLM honeypot process was running:

```bash
ps -ef | grep ssh_honeypot | grep -v grep
```

```bash
ps aux | grep ssh_honeypot.py
```

## 6. Checking the Listening Port

The following commands were used to check whether the honeypot was listening on port `2222`:

```bash
sudo ss -tulnp | grep 2222
```

```bash
ss -tlnp | grep 2222
```

## 7. Stopping the LLM Honeypot

The following command was used to stop the running LLM honeypot process:

```bash
pkill -f ssh_honeypot.py
```

## 8. Checking Ollama Status

The following command was used to check whether the Ollama service was running:

```bash
systemctl status ollama --no-pager
```

## 9. Checking LLM Honeypot Logs

The following commands were used to inspect the LLM honeypot log file:

```bash
tail -f ssh_honeypot.log
```

```bash
tail -n 50 ssh_honeypot.log
```

```bash
less ssh_honeypot.log
```

The following command was used to inspect a JSONL log file from the `logs` folder:

```bash
tail -n 50 logs/20260423_133921.jsonl
```

## 10. Checking Run Logs

The following commands were used to inspect run log files created when the honeypot was launched in the background:

```bash
tail -10 honeypot_run.log
```

```bash
tail -n 50 honeypot_run_attacker5.log
```
