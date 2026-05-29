# LLM Honeypot Python Files

This file documents the main Python files used by the current LLM-based honeypot setup. These files supported SSH handling, LLM response generation, command correction, dataset loading, and logging.

## 1. Listing Active Python Files

The following command was used to list the active Python files in the LLM honeypot project folder:

```bash
ls -lh honeypot.py ssh_honeypot.py
```

The active Python files were:

```text
honeypot.py
ssh_honeypot.py
```

## 2. Checking SSH Honeypot Script Logic

The following command was used to inspect important SSH-related code references inside `ssh_honeypot.py`:

```bash
grep -nEi "import|HOST|PORT|HOST_KEY_PATH|paramiko|class |def |check_auth_password|handle_client|start_server|bind|listen" ssh_honeypot.py
```

## 3. SSH Honeypot Script

The `ssh_honeypot.py` file handled the SSH honeypot interface. It used Paramiko to accept SSH connections and listen on port `2222`.

The script included key SSH-related elements such as:

```text
paramiko
HOST = "0.0.0.0"
PORT = 2222
HOST_KEY_PATH = "/home/llmhoneypot/llmhoneypot_v2/host_rsa.key"
class HoneypotServer(paramiko.ServerInterface)
check_auth_password
check_channel_request
check_channel_pty_request
check_channel_shell_request
handle_client
start_server
sock.bind((HOST, PORT))
sock.listen(100)
```

## 4. Checking LLM Command Handling Logic

The following command was used to inspect important LLM, correction, filesystem, attack pattern, and logging references inside `honeypot.py`:

```bash
grep -nEi "import|ollama|ask_ollama|corrections|filesystem|attack_patterns|log_event|jsonl|command_output|subprocess|def |class " honeypot.py
```

## 5. LLM Command Handling Script

The `honeypot.py` file handled the LLM-based command response logic. It included references to Ollama response generation, corrected command outputs, simulated filesystem data, attack pattern data, built-in command handling, and JSONL logging.

The script included references such as:

```text
OLLAMA_URL = "http://127.0.0.1:11434/api/generate"
ask_ollama(prompt)
load_filesystem()
load_corrections()
load_attack_patterns()
build_prompt(...)
builtin_output(...)
log_event(...)
command_output
```

## 6. Purpose of Python Files

These Python files formed the main implementation of the current LLM-based honeypot. The SSH script handled incoming SSH connections, authentication handling, host key usage, and port binding. The main honeypot script supported LLM-generated command responses, correction handling, simulated filesystem behaviour, attack pattern handling, built-in command handling, and structured logging.
