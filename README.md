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


# Task 2: User Management and Access Control

# Commands :

# TASK 2 COMMANDS :

sudo adduser Sarah

sudo adduser Mike

sudo passwd Sarah  

sudo passwd Mike    

sudo mkdir /home/Sarah/workspace

sudo chown Sarah:Sarah /home/Sarah/workspace

sudo chmod 700 /home/Sarah/workspace

sudo mkdir /home/Mike/workspace

sudo chown Mike:Mike /home/Mike/workspace

sudo chmod 700 /home/Mike/workspace

sudo chage -M 30 Sarah
sudo chage -M 30 Mike
sudo chage -l Sarah
sudo chage -l Mike

# Changed the settings in following path 
sudo nano /etc/login.defs - # password length (12 characters)
sudo nano /etc/security/pwquality.conf

# Changed the settings in following path /etc/pam.d/system-auth and /etc/pam.d/password-auth:
password    requisite     pam_pwquality.so retry=3


# Screenshot of the output :

# TASK 2 OUTPUT :

# Setting up the Directories:-

<img width="768" height="258" alt="image" src="https://github.com/user-attachments/assets/4d115261-b683-4639-8ef2-90bc1c6d42ff" />

<img width="712" height="277" alt="image" src="https://github.com/user-attachments/assets/ff9fc788-3926-4943-8071-17047364fe70" />

# Enforcing password policy to users(Sarah & Mike)

<img width="797" height="478" alt="image" src="https://github.com/user-attachments/assets/75cfd175-82f8-461f-bcb3-d1cd33b17849" />

# Configrations files changes made following length, lowercase, uppercase and digits

<img width="1021" height="677" alt="image" src="https://github.com/user-attachments/assets/c12a6e9e-a43c-4ca1-8218-4f2b58a0f725" />

# Password Complexity check

<img width="1037" height="113" alt="image" src="https://github.com/user-attachments/assets/df85ba40-03b4-4440-9417-93d3e0c5768c" />

<img width="487" height="118" alt="image" src="https://github.com/user-attachments/assets/7bb49343-0e02-4501-9c7c-ab4a686d311d" />



# Task 3: Backup Configuration for Web Servers

# Commands :

# TASK 3 COMMANDS :

# Apache server setup

sudo yum install httpd -y # Install Apache

sudo systemctl enable httpd

sudo systemctl start httpd

sudo systemctl status httpd

# Nginx server setup

sudo yum install nginx -y # Install Nginx

sudo systemctl enable nginx

sudo systemctl start nginx

sudo systemctl status nginx

# o	Sarah: Backup the Apache configuration (/etc/httpd/) and document root (/var/www/html/)

cd /home/Sarah/

nano apache_backup.sh

#!/bin/bash
DATE=$(date +%F)
BACKUP_DIR="/backups"
BACKUP_FILE="$BACKUP_DIR/apache_backup_$DATE.tar.gz"

# Create backup

tar -czf $BACKUP_FILE /etc/httpd/ /var/www/html/

# Verify backup

tar -tzf $BACKUP_FILE > $BACKUP_DIR/apache_backup_${DATE}_verify.log

# o	Mike: Backup the Nginx configuration (/etc/nginx/) and document root (/usr/share/nginx/html/)

cd /home/mike/

nano nginx_backup.sh

#!/bin/bash
DATE=$(date +%F)
BACKUP_DIR="/backups"
BACKUP_FILE="$BACKUP_DIR/nginx_backup_$DATE.tar.gz"

# Create backup
tar -czf $BACKUP_FILE /etc/nginx/ /usr/share/nginx/html/
# Verify backup
tar -tzf $BACKUP_FILE > $BACKUP_DIR/nginx_backup_${DATE}_verify.log

sudo chmod +x /home/Sarah/apache_backup.sh

sudo chmod +x /home/mike/nginx_backup.sh

# Schedule Cron Jobs

sudo crontab -u Sarah -e
sudo crontab -u Mike -e


# Screenshot of the output :

# TASK 3 OUTPUT :

<img width="692" height="21" alt="image" src="https://github.com/user-attachments/assets/8e9a6b28-93aa-4b38-a46f-42c71f0a67c0" />

<img width="1221" height="838" alt="image" src="https://github.com/user-attachments/assets/ac52706d-9152-4c65-bd3f-1c59e38754c3" />

<img width="665" height="102" alt="image" src="https://github.com/user-attachments/assets/7d51aaa5-7172-4148-982b-128172fb2cab" />

<img width="1400" height="762" alt="image" src="https://github.com/user-attachments/assets/1cff99f4-6086-4487-a47f-d385ba657ade" />



# Schedule Cron Jobs

<img width="1838" height="1018" alt="image" src="https://github.com/user-attachments/assets/51278c9a-61fa-4a71-815f-efcbbb8957c6" />

<img width="1892" height="1011" alt="image" src="https://github.com/user-attachments/assets/db098e2a-7da8-4ff1-94d7-4ea1f3252229" />


# Backup file creations

<img width="960" height="407" alt="image" src="https://github.com/user-attachments/assets/f56896e4-3ddd-4537-963c-f851c2a9e8f3" />


# Backup files or verification logs :

# Apache Server

<img width="741" height="565" alt="image" src="https://github.com/user-attachments/assets/3315ed89-f9c5-4fcc-bc3d-302e1bed4761" />

# Nginx Server

<img width="882" height="568" alt="image" src="https://github.com/user-attachments/assets/4a781d07-d7ad-4c9c-a45a-88b763ab1a5b" />

