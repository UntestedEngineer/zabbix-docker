## Modified Zabbix Docker

This repository is a fork of the original located here: [Zabbix Docker](https://github.com/zabbix/zabbix-docker)

## Summary
The docker files for the server component have a few additional packages installed to support [UniFi Zabbix](https://github.com/patricegautier/unifiZabbix)

### Changes
The following packages are installed into the "Dockerfiles > server-pgsql" docker files since I only use a pgsql backend.  As I maintain only the Ubuntu and Alpine variants I have removed the rest of the distribution folders:

            openssh-client 
            jq 
            expect