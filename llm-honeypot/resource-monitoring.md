# LLM Honeypot Resource Monitoring Commands

This file documents the resource monitoring commands used for the LLM-based honeypot. These commands were used to record CPU usage, RAM usage, and available memory while the LLM honeypot was running.

## 1. Confirming the Working Directory

The following command was used to confirm the current working directory:

```bash
pwd
```

The working directory was:

```text
/home/llmhoneypot
```

## 2. Recording LLM Resource Usage

The following command was used to record CPU usage, RAM usage, and available memory into an LLM usage log file:

```bash
nohup bash -c 'while true; do echo "$(date "+%F %T") CPU_USED=$(top -bn1 | awk "/Cpu/ {printf \"%.2f\", 100-\$8}")% RAM_USED=$(free | awk "/Mem:/ {printf \"%.2f\", \$3/\$2*100}")% AVAIL_MB=$(free -m | awk "/Mem:/ {print \$7}")"; sleep 1; done' >> llm_usage_attacker5.log 2>&1 &
```

## 3. Checking the Resource Usage Log

The following command was used to check the latest entries in the LLM resource usage log:

```bash
tail -5 llm_usage_attacker5.log
```

The following command was also used to inspect more entries from the same log file:

```bash
tail -20 llm_usage_attacker5.log
```

## 4. Extracting Peak CPU Usage

The following command was used to extract the highest recorded CPU usage value from the LLM usage log:

```bash
echo "PEAK_CPU_PERCENT=$(grep -o 'CPU_USED=[0-9.]*%' llm_usage_attacker5.log | cut -d= -f2 | tr -d '%' | sort -nr | head -1)%"
```

## 5. Extracting Peak RAM Usage

The following command was used to extract the highest recorded RAM usage value from the LLM usage log:

```bash
echo "PEAK_RAM_PERCENT=$(grep -o 'RAM_USED=[0-9.]*%' llm_usage_attacker5.log | cut -d= -f2 | tr -d '%' | sort -nr | head -1)%"
```

## 6. Extracting Lowest Available RAM

The following command was used to extract the lowest available RAM value from the LLM usage log:

```bash
echo "LOWEST_AVAILABLE_RAM_MB=$(grep -o 'AVAIL_MB=[0-9]*' llm_usage_attacker5.log | cut -d= -f2 | sort -n | head -1)"
```

## 7. Stopping the Resource Monitoring Log

The following command was used to stop the running LLM resource monitoring process:

```bash
pkill -f llm_usage_attacker5.log
```

## 8. Purpose of Monitoring

These commands were used to record and analyse the resource usage of the LLM-based honeypot during testing. The collected CPU, RAM, and available memory values were later used to compare the LLM-based honeypot against the traditional Cowrie honeypot.
