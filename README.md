# System-Health-Monitoring-Script-
#Python 3.x
#psutil library (to gather system statistics)
#Logging for alerts

import psutil
import logging

# Set up logging
logging.basicConfig(filename='system_health.log', level=logging.INFO,
                    format='%(asctime)s - %(levelname)s - %(message)s')

# Thresholds
CPU_THRESHOLD = 80  # percent
MEMORY_THRESHOLD = 80  # percent
DISK_THRESHOLD = 80  # percent

def check_cpu_usage():
    usage = psutil.cpu_percent(interval=1)
    if usage > CPU_THRESHOLD:
        logging.warning(f"High CPU usage detected: {usage}%")
    return usage

def check_memory_usage():
    memory = psutil.virtual_memory()
    usage = memory.percent
    if usage > MEMORY_THRESHOLD:
        logging.warning(f"High memory usage detected: {usage}%")
    return usage

def check_disk_usage():
    disk = psutil.disk_usage('/')
    usage = disk.percent
    if usage > DISK_THRESHOLD:
        logging.warning(f"Low disk space detected: {usage}% used")
    return usage

def check_running_processes():
    processes = len(psutil.pids())
    logging.info(f"Number of running processes: {processes}")
    return processes

def main():
    cpu = check_cpu_usage()
    memory = check_memory_usage()
    disk = check_disk_usage()
    processes = check_running_processes()

    print(f"CPU Usage: {cpu}%")
    print(f"Memory Usage: {memory}%")
    print(f"Disk Usage: {disk}%")
    print(f"Running Processes: {processes}")

if __name__ == "__main__":
    main()
