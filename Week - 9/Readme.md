# Project 7 - Setting Up a HoneyPot

1. HoneyPot Deployed:
 - Ubuntu - Dionaea with HTTP

2. Issues Encountered:
 - Setting up GCP VM for mhn-admin: Do not use machine type as "f1-micro" for mhn admin machines. This causes mhn installation script to fail after the "Path for log file" prompt. Possible cause of issue here low memory in f1-micro instances. Please use machine type as "g1-small" instead. This also speeds up set up and installation processes.
 - After success installation the following output should be seen for 'sudo supervisorctl status':
 ```
geoloc                           RUNNING    pid 31443, uptime 0:00:12
honeymap                         RUNNING    pid 30826, uptime 0:08:54
hpfeeds-broker                   RUNNING    pid 10089, uptime 0:36:42
mhn-celery-beat                  RUNNING    pid 29909, uptime 0:18:41
mhn-celery-worker                RUNNING    pid 29910, uptime 0:18:41
mhn-collector                    RUNNING    pid 7872,  uptime 0:18:41
mhn-uwsgi                        RUNNING    pid 29911, uptime 0:18:41
mnemosyne                        RUNNING    pid 28173, uptime 0:30:08
 ```
 But this is the output obtained:
 ```
geoloc                           RUNNING    pid 4047, uptime 0:03:42
honeymap                         RUNNING    pid 4051, uptime 0:03:42
hpfeeds-broker                   RUNNING    pid 4045, uptime 0:03:42
mhn-celery-beat                  RUNNING    pid 4044, uptime 0:03:42
mhn-celery-worker                FATAL      Exited too quickly (process log may have details)
mhn-collector                    RUNNING    pid 4050, uptime 0:03:42
mhn-uwsgi                        RUNNING    pid 4048, uptime 0:03:42
mnemosyne                        RUNNING    pid 4046, uptime 0:03:42
 ```
 Checking the logs with "tail -f /var/log/mhn/mhn-celery-worker.*" would display the following line at the end:
 ```
 VersionMismatch(‘Redis transport requires redis-py versions 3.2.0 or later. You have 2.10.6’,)
 ```
 This can be fixed by removing the current version of redis and installing the latest version of redis using pip.
 Restart mhn-celery-worker using "sudo supervisorctl start mhn-celery-worker"

3. Summary of HoneyPot Data:
 - Total time HoneyPot is active: 30 minutes.
 - Total attacks: 1025
 - JSON Output file: Available in root folder
