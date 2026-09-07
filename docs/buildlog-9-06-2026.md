# Day Log — Zabbix Installation and Configuration

**Date:** September 7, 2026

## Objective

Continue building my Ubuntu Server home lab by completing the Zabbix database setup and accessing the monitoring dashboard.

## Work Completed

- Confirmed the Zabbix packages were installed
- Located the correct Zabbix SQL schema file
- Imported the Zabbix schema into MySQL
- Verified that the database contained 203 tables
- Added the database password to the Zabbix server configuration
- Restarted and verified the Zabbix server
- Confirmed Zabbix Agent 2 and Nginx were running
- Configured the Zabbix frontend to use TCP port 8080
- Tested the Nginx configuration
- Confirmed the frontend redirected successfully to `setup.php`
- Allowed port 8080 through UFW
- Completed the Zabbix browser setup
- Logged into the Zabbix dashboard

## Commands Used

### Check installed Zabbix packages

```bash
dpkg -l | grep zabbix
```

### Locate the database schema

```bash
dpkg -L zabbix-sql-scripts | grep server.sql
```

### Import the schema

```bash
zcat /usr/share/zabbix-sql-scripts/mysql/server.sql.gz | mysql --default-character-set=utf8mb4 -u zabbix -p zabbix
```

### Verify the database import

```bash
mysql -u zabbix -p -e "SELECT COUNT(*) AS table_count FROM information_schema.tables WHERE table_schema='zabbix';"
```

**Result:** 203 tables

### Edit the Zabbix server configuration

```bash
sudo nano /etc/zabbix/zabbix_server.conf
```

Added the following setting without documenting the actual password:

```text
DBPassword=[REDACTED]
```

### Restart and verify Zabbix

```bash
sudo systemctl restart zabbix-server
sudo systemctl status zabbix-server --no-pager
systemctl is-active zabbix-agent2 nginx
```

**Result:** All services were active.

### Configure and test the web frontend

```bash
sudo nano /etc/zabbix/nginx.conf
sudo nginx -t
sudo systemctl restart nginx
curl -I http://localhost:8080
```

The Zabbix Nginx configuration was set to:

```text
listen 8080;
server_name _;
```

**Result:** `HTTP/1.1 302 Found` with a redirect to `setup.php`.

### Verify the firewall rule

```bash
sudo ufw allow 8080/tcp
```

**Result:** The rule already existed.

## Troubleshooting

The original instructions listed the schema at:

```text
/usr/share/zabbix/sql-scripts/mysql/server.sql.gz
```

That file did not exist on my system. I used the package file list to find the correct location:

```text
/usr/share/zabbix-sql-scripts/mysql/server.sql.gz
```

The database initially contained zero tables. After importing the correct schema, it contained 203 tables.

I also corrected a SQL query that used `information_schema.table` instead of the correct `information_schema.tables`.

## What I Learned

- How Zabbix stores monitoring information in MySQL
- How to locate files installed by an Ubuntu package
- How to import a compressed SQL schema
- How to configure services using files in `/etc`
- How to verify services with `systemctl`
- How to test an Nginx configuration before restarting it
- How HTTP redirects can confirm that a web application is responding
- How to expose a service safely through a specific firewall port

## Screenshots

- Zabbix package list
- Successful database table count
- Active Zabbix server status
- Successful Nginx configuration test
- Zabbix login page
- Zabbix dashboard

> Passwords and sensitive configuration values were excluded from all screenshots.
>
## Monitoring Validation Test

I verified that Zabbix was collecting live performance data by generating a controlled CPU load on the Ubuntu VM:

```bash
yes > /dev/null

I allowed Zabbix to collect data points, stopped the test with Ctrl+C, and confirmed that the CPU graph was showing me information about the utilization

During testing the dashboard initially said that the Zabbix server wasnt running it showed
```bash
Access denied for user 'zabbix'@'localhost' (using password: NO)

I corrected the DB password setting, restarted the zabbix-server, and confirmed that live monitoring was working.

