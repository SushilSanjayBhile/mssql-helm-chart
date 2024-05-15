# MSSQL Custom Helm Chart

This Helm chart is designed to deploy MSSQL in a Kubernetes environment. It provides configurations to customize the deployment according to your needs.

## References

Docker image used from dockerhub microsoft-mssql-server repository:
https://hub.docker.com/_/microsoft-mssql-server

Docker deployment and MSSQL database testing reference document:
https://hub.docker.com/_/microsoft-mssql-server

## Installation of Helm chart

Using app catalog you can install MSSQL helm chart
Once installation is successful, exec inside the container and create DB and add records in the newly created DB.

Please refer below 'Installation of docker container' section for commands.  

## Installation of docker container

To install the MSSQL docker container and to test it's validity, run the following command:

```bash
$ docker pull mcr.microsoft.com/mssql/server:2022-preview-ubuntu-22.04
$ docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=yourStrong(!)Password" -e "MSSQL_PID=Evaluation" -p 1433:1433  --name sqlpreview --hostname sqlpreview -d mcr.microsoft.com/mssql/server:2022-preview-ubuntu-22.04
$ docker exec -ti sqlpreview sh
$ apt update -y
$ apt install vim -y
$ apt install sudo -y
$ vi createdb.sh   (https://github.com/microsoft/mssql-docker/blob/master/linux/preview/examples/mssql-customize/configure-db.sh)
$ vi setup.sql (https://github.com/microsoft/mssql-docker/blob/master/linux/preview/examples/mssql-customize/setup.sql) 
 
$ /opt/mssql-tools/bin/sqlcmd -S localhost -U sa -P $SA_PASSWORD -d master -i setup.sql
# Msg 1801, Level 16, State 3, Server sqlpreview, Line 7
# Database 'HelloWorld' already exists. Choose a different database name.

$ /opt/mssql-tools/bin/sqlcmd -S localhost -U sa -P Diamanti@111 -d HelloWorld -Q "SELECT 1"   
# -----------
#          1
#
# (1 rows affected)
#

$ /opt/mssql-tools/bin/sqlcmd -?
# Microsoft (R) SQL Server Command Line Tool
# Version 17.10.0001.1 Linux
# Copyright (C) 2017 Microsoft Corporation. All rights reserved.

# usage: sqlcmd            [-U login id]          [-P password]
#   [-S server or Dsn if -D is provided] 
#   [-H hostname]          [-E trusted connection]
#   [-N Encrypt Connection][-C Trust Server Certificate]
#   [-d use database name] [-l login timeout]     [-t query timeout]
#   [-h headers]           [-s colseparator]      [-w screen width]
#   [-a packetsize]        [-e echo input]        [-I Enable Quoted Identifiers]
#   [-c cmdend]
#   [-q "cmdline query"]   [-Q "cmdline query" and exit]
#   [-m errorlevel]        [-V severitylevel]     [-W remove trailing spaces]
#   [-u unicode output]    [-r[0|1] msgs to stderr]
#   [-i inputfile]         [-o outputfile]
#   [-k[1|2] remove[replace] control characters]
#   [-y variable length type display width]
#   [-Y fixed length type display width]
#   [-p[1] print statistics[colon format]]
#   [-R use client regional setting]
#   [-K application intent]
#   [-M multisubnet failover]
#   [-b On error batch abort]
#   [-D Dsn flag, indicate -S is Dsn] 
#   [-X[1] disable commands, startup script, environment variables [and exit]]
#   [-x disable variable substitution]
#   [-g enable column encryption]
#   [-G use Azure Active Directory for authentication]
#   [-? show syntax summary]
```


## Authors

- [@SushilSanjayBhile](https://github.com/SushilSanjayBhile)

