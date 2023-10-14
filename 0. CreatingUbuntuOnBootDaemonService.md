#Steps for creating a ubuntu on boot daemon service

Step 1 : Navigate to 
```
cd /lib/systemd/system"
```
Step 2 : Create .service file with any name
``` 
vi mysqldb.service
```
Step 3 : Write and Quit the below script in mysqldb.service file
```
[Unit]
#Description can be any name
Description=MySQL_SpringBoot_App
After=syslog.target network.target

[Service]
SuccessExitStatus=143
User=root
#provide your jar target path
ExecStart=java -jar /home/ubadmin/spring-boot-mysql-example/target/spring-boot-mysql-0.0.1-SNAPSHOT.jar
Restart=on-failure

[Install]
WantedBy=multi-user.target
```
Step 4 : Run below command to create system link
```
systemctl enable mysqldb.service
```
Step 5 : Run below command 
```
systemctl daemon-reload
```
Note: The above command should be run whenever you make changes to the service file else not required.

Step 6 : Run below command to start the service
```
systemctl start mysqldb.service
```
Step 7 : Run below command to verify the status
```
systemctl status mysqldb.service --no-pager 
```
Step 8 : Browse the link
```
yourhostip:port
```