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
A summary of the data collected: number of attacks, number of malware samples, etc.
Any unresolved questions raised by the data collected
