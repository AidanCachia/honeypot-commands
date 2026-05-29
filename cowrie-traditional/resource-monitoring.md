# Cowrie Resource Monitoring Commands

This file documents the resource monitoring commands used for the traditional Cowrie honeypot. These commands were used to calculate peak CPU usage, estimated peak RAM usage, and lowest free memory during local testing.

## 1. Creating the Monitoring Folder

The following command was used to create the monitoring log folder:

```bash
mkdir -p ~/monitor_logs
```

## 2. Entering the Monitoring Folder

The following command was used to enter the monitoring log folder:

```bash
cd ~/monitor_logs
```

## 3. Recording VMStat Data

The following command was used to record VMStat output into a Cowrie monitoring log file:

```bash
vmstat 1 > cowrie_vmstat.log
```

This command records VMStat output every second and saves it into `cowrie_vmstat.log`. The recording was stopped manually using `Ctrl + C` after the test session was completed.

## 4. Checking the Monitoring Folder

The following command was used to check the contents of the monitoring folder:

```bash
ls -lh ~/monitor_logs
```

## 5. Previewing the VMStat Log

The following commands were used to preview the beginning and end of the Cowrie VMStat log file:

```bash
head ~/monitor_logs/cowrie_vmstat.log
```

```bash
tail ~/monitor_logs/cowrie_vmstat.log
```

## 6. Calculating Peak CPU Usage

The following command was used to calculate the peak CPU usage from the Cowrie VMStat log:

```bash
awk '$1 ~ /^[0-9]+$/ {print $13+$14}' ~/monitor_logs/cowrie_vmstat.log | sort -nr | head -1 | awk '{printf("Peak CPU Usage: %.0f%%\n",$1)}'
```

Example output:

```text
Peak CPU Usage: 3%
```

## 7. Calculating Estimated Peak RAM Usage

The following command was used to calculate estimated peak RAM usage from the Cowrie VMStat log. The calculation assumes that the VM had 4096 MB of allocated RAM:

```bash
awk '$1 ~ /^[0-9]+$/ {used=(4096-($4/1024)); pct=(used/4096)*100; print pct}' ~/monitor_logs/cowrie_vmstat.log | sort -nr | head -1 | awk '{printf("Estimated Peak RAM Usage: %.1f%%\n",$1)}'
```

Example output:

```text
Estimated Peak RAM Usage: 37.6%
```

## 8. Calculating Lowest Free Memory

The following command was used to calculate the lowest free memory value from the Cowrie VMStat log:

```bash
awk '$1 ~ /^[0-9]+$/ {print $4/1024}' ~/monitor_logs/cowrie_vmstat.log | sort -n | head -1 | awk '{printf("Lowest Free Memory: %.1f MB\n",$1)}'
```

Example output:

```text
Lowest Free Memory: 2556.6 MB
```

## 9. Purpose of Monitoring

These commands were used to record and analyse the resource usage of the traditional Cowrie honeypot during local testing. The values collected from this process were later used to compare Cowrie's CPU and memory usage with the LLM-based honeypot.
