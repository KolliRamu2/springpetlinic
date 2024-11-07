## Manual steps for Ubuntu
* sudo apt update
* sudo apt install openjdk-17-jdk -y
* sudo useradd -d /var/lib/spc -m -p spc -s /bin/sh spc
* sudo wget -P /var/lib/spc/ https://referenceappslt.s3.ap-south-1.amazonaws.com/spring-petclinic-3.3.0-SNAPSHOT.jar
* sudo -i
* sudo cd /var/lib/spc/
* sudo chown spc:spc spring-petclinic-3.3.0-SNAPSHOT.jar
* sudo vi /usr/lib/systemd/system/spc.service
```
[Unit]
Description=Run spring petlinic
After=network-online.target remote-fs.target nss-lookup.target
Wants=network-online.target

[Service]
Type=simple
PIDFile=/run/spring-petclinic-3.3.0-SNAPSHOT.jar.pid
ExecStart=/usr/bin/java -jar /var/lib/spc/spring-petclinic-3.3.0-SNAPSHOT.jar 'daemon on; master_process on;'
ExecStop=-/sbin/start-stop-daemon --quiet --stop --retry QUIT/5 --pidfile /run/spring-petclinic-3.3.0-SNAPSHOT.jar.pid

TimeoutStopSec=5
KillMode=mixed

[Install]
WantedBy=multi-user.target
```
* sudo systemctl daemon-reload
* sudo systemctl enable spc.service
* sudo systemctl start spc.service
## Additional commands for reference
* sudo ls -la /var/lib/spc/
* sudo -i
* sudo cd /var/lib/spc/
* sudo apt search openjdk
* sudo apt-cache search java
* whereis java

# Manual steps for Redhat
* sudo dnf update -y
* sudo dnf install  java-17-openjdk -y
* sudo useradd -d /var/lib/spc -m -p spc -s /bin/sh spc
* sudo dnf install wget -y
* sudo wget -P /var/lib/spc/ https://referenceappslt.s3.ap-south-1.amazonaws.com/spring-petclinic-3.3.0-SNAPSHOT.jar
* sudo chown spc:spc spring-petclinic-3.3.0-SNAPSHOT.jar
* sudo vi /usr/lib/systemd/system/spc.service
```
[Unit]
Description=Run spring petlinic
After=network-online.target remote-fs.target nss-lookup.target
Wants=network-online.target

[Service]
Type=simple
PIDFile=/run/spring-petclinic-3.3.0-SNAPSHOT.jar.pid
ExecStart=/usr/bin/java -jar /var/lib/spc/spring-petclinic-3.3.0-SNAPSHOT.jar 'daemon on; master_process on;'
ExecStop=-/sbin/start-stop-daemon --quiet --stop --retry QUIT/5 --pidfile /run/spring-petclinic-3.3.0-SNAPSHOT.jar.pid

TimeoutStopSec=5
KillMode=mixed

[Install]
WantedBy=multi-user.target
```
* sudo systemctl daemon-reload
* sudo systemctl enable spc.service
* sudo systemctl start spc.service

## Additional commands
* sudo yum list available *openjdk*
* 