# Assignment-on-Testing-Linux-and-Servers_Raja-V

# Task 1: System Monitoring Setup

Install and configure htop or nmon to monitor CPU, memory, and processes, using df and du for disk usage tracking, and identifying resource-intensive processes. Proper logging of system metrics and clear documentation of the setup are essential. 

# Commands :

# TASK 1 COMMANDS :

**1.	Install and configure monitoring tools (htop or nmon) to monitor CPU, memory, and process usage.**

sudo dnf install htop - *** Install the htop ***

sudo dnf install nmon - *** Install the nmon ***

nano system_health.sh *** Creating Shell file ***

*** system_health.sh ***
#!/bin/bash
echo "==== $(date) ====" >> /var/log/system_health.log
htop -b -n 1 >> /var/log/system_health.log     # htop batch mode, one iteration
df -h >> /var/log/system_health.log
du -sh /home/* >> /var/log/system_health.log
ps -eo pid,comm,%cpu,%mem --sort=-%cpu | head -10 >> /var/log/system_health.log


# Screenshot of the output :

# TASK 1 OUTPUT :

<img width="957" height="931" alt="image" src="https://github.com/user-attachments/assets/dfcd6db2-7555-486f-9193-eb8dff78dc19" />

<img width="1912" height="1078" alt="image" src="https://github.com/user-attachments/assets/927718bd-2be5-4c51-b85a-7547b969080f" />

<img width="1905" height="690" alt="image" src="https://github.com/user-attachments/assets/be30424e-a52f-47f3-93af-125711a2537a" />

<img width="1912" height="1076" alt="image" src="https://github.com/user-attachments/assets/8c006751-07cd-410a-a074-eb6214285dad" />

<img width="1918" height="1078" alt="image" src="https://github.com/user-attachments/assets/7ab81e17-73ee-4c94-91f1-3442131a3271" />

<img width="1911" height="1078" alt="image" src="https://github.com/user-attachments/assets/e6760eeb-6c52-441e-8164-7b1917b27fc5" />

<img width="1312" height="310" alt="image" src="https://github.com/user-attachments/assets/29157868-ab95-414e-a646-17b8a8fcc2d6" />

<img width="1917" height="1078" alt="image" src="https://github.com/user-attachments/assets/f6807087-74b8-4389-b785-84a884d114cd" />

# Download the logs in the Windows system :

<img width="1177" height="113" alt="image" src="https://github.com/user-attachments/assets/23321750-f28c-4e7d-80f4-ee82e1df0b00" />

# Task 1 - Log files output 

<img width="1901" height="1078" alt="image" src="https://github.com/user-attachments/assets/2223f959-e046-4f13-b2d7-66978e5a5c90" />


