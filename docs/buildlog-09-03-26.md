## Home Lab Progress — September 3, 2026

### Project Goal

Build a network-monitoring lab using Zabbix on an Ubuntu Server virtual machine. The completed lab will monitor server health, network availability, services, and additional devices such as a Raspberry Pi/Pi-hole.

### Existing Environment

* Oracle VirtualBox
* Ubuntu Server 26.04.1 LTS
* Zabbix 7.0 LTS
* MariaDB 11.8.6
* Nginx web server
* UFW firewall
* Windows host computer
* Raspberry Pi running Pi-hole

### VirtualBox Network Configuration

The Ubuntu VM has two network interfaces:

* `enp0s3` - NAT adapter

  * IP address: `10.0.2.15`
  * Provides internet access to the VM
  * Default gateway: `10.0.2.2`

* `enp0s8` - Host-only adapter

  * IP address: `192.168.56.101`
  * Provides private communication between the Windows host and Ubuntu VM
  * Used for SSH and browser access to hosted services

### Connectivity Testing

Network connectivity was verified with the following tests:

* Successfully pinged `8.8.8.8`
* Successfully resolved and pinged `google.com`
* Recorded 0% packet loss during both tests
* Confirmed that both internet connectivity and DNS resolution were working

### Existing Services

Nginx was verified as:

* Installed
* Enabled at startup
* Active and running
* Hosting a custom Ubuntu home-lab webpage

### Firewall Configuration

UFW is active with a default policy of:

* Deny incoming traffic
* Allow outgoing traffic

The following inbound ports are currently allowed:

* TCP 22 - SSH
* TCP 80 - Nginx HTTP
* TCP 8080 - Previous HTTP lab service

Firewall rules will be reviewed and restricted as the monitoring lab is completed.

### System Resources

The Ubuntu VM currently has:

* Approximately 7.3 GB RAM
* Approximately 6 GB available RAM
* 25 GB root filesystem
* Approximately 17 GB available storage
* Approximately 28% disk utilization

These resources are sufficient for the planned Zabbix monitoring lab.

### Safety and Recovery

A VirtualBox snapshot named `Before Zabbix Installation` was created before installing the monitoring platform. This provides a recovery point if the installation or configuration causes problems.

### Zabbix Installation Completed

The official Zabbix 7.0 repository for Ubuntu 26.04 was added successfully.

The following packages were installed and verified:

* `zabbix-server-mysql`
* `zabbix-frontend-php`
* `zabbix-nginx-conf`
* `zabbix-sql-scripts`
* `zabbix-agent2`
* `zabbix-release`
* `mariadb-server`

MariaDB was confirmed to be enabled and actively running.

### Database Preparation Completed

A dedicated MariaDB database and local database account were created for Zabbix.

Completed database tasks:

* Created the `zabbix` database
* Configured UTF-8 database encoding
* Created the local `zabbix` database user
* Granted the required database privileges
* Temporarily enabled trusted function creation for the schema import

Database passwords were excluded from screenshots and documentation.

### Current Checkpoint

The Zabbix database schema has not yet been imported.

The expected `server.sql.gz` path was not found, so the next step is to locate the SQL schema installed by the `zabbix-sql-scripts` package and rerun the import using its actual path.

### Skills Practiced

* Linux server administration
* VirtualBox networking
* NAT and host-only networking
* SSH remote administration
* Firewall configuration with UFW
* Nginx service management
* Network connectivity testing
* Package and repository management
* MariaDB administration
* Monitoring-platform deployment
* Troubleshooting Linux file paths
* Technical documentation
