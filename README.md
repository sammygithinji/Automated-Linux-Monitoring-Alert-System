# Linux Monitoring & Alerting System with Bash | Server Monitoring, Email Alerts, and Automation

## Lightweight Linux Server Monitoring Tool for DevOps, Uptime Monitoring, and Failure Detection

Never wake up to a crashed server again.

This project is a **Linux server monitoring and alerting system built with Bash scripting** that continuously checks the health of critical services such as NGINX, SSH, and MySQL. It performs **automated service monitoring, failure detection, and real-time email alerting** using Postfix and Gmail SMTP.

Designed for **DevOps engineers, Linux administrators, and site reliability roles**, this system demonstrates practical implementation of **uptime monitoring, incident response, and infrastructure automation** without relying on heavy external tools.

## System Overview

```text
Server → monitor.sh → Service Check → Failure?
                         │
                YES ─────┴───── NO
                 │              │
         Send Email Alert    Continue Monitoring
                 │
              Log Event
```

## User Instructions (Quick Setup)

### 1. Clone and Prepare

```bash
git clone https://github.com/your-username/linux-monitoring-alert-system.git
cd linux-monitoring-alert-system
chmod +x monitor.sh
```

### 2. Install Dependencies

```bash
sudo apt update
sudo apt install postfix mailutils -y
```

### 3. Configure Email Alerts

```bash
sudo nano /etc/postfix/sasl_passwd
```

Add:

```
[smtp.gmail.com]:587 your-email@gmail.com:your-app-password
```

Apply configuration:

```bash
sudo chmod 600 /etc/postfix/sasl_passwd
sudo postmap /etc/postfix/sasl_passwd
sudo systemctl restart postfix
```

### 4. Set Alert Email

```bash
nano monitor.sh
```

Update:

```bash
ALERT_EMAIL="your-email@gmail.com"
```

### 5. Test the System

```bash
./monitor.sh
sudo systemctl stop nginx
```

### 6. Automate with Cron

```bash
crontab -e
```

Add:

```
*/5 * * * * /home/$USER/linux-monitoring-alert-system/monitor.sh
```

##  Developer Notes

### Project Structure

```
linux-monitoring-alert-system/
├── monitor.sh
├── README.md
├── .gitignore
```

### Core Implementation

* `systemctl is-active` → service health checks
* Bash scripting → automation logic
* Postfix → email delivery
* Cron → scheduling
* Log files → event tracking

### Extending the System

Monitor multiple services:

```bash
SERVICES=("nginx" "mysql" "ssh")
```

Add webhook alerts:

```bash
curl -X POST https://your-api.com/webhook \
-d "{\"service\":\"nginx\",\"status\":\"down\"}"
```

##  Expected Behavior

| Event            | Result              |
| ---------------- | ------------------- |
| Service running  | No alert            |
| Service fails    | Email sent          |
| Service recovers | Logged              |
| Repeated failure | No duplicate alerts |

##  Known Issues

* Gmail requires App Password authentication
* Emails may initially go to spam
* Cron jobs require absolute paths
* Limited by SMTP rate limits (Gmail)

##  Contributing

* Fork the repository
* Create a feature branch
* Submit a pull request

##  Support

If this project helped you implement Linux monitoring or improve your DevOps workflow, you can support its development.

Small contributions help maintain and expand practical open-source tools like this.
Starring or sharing the project is equally appreciated.

##  License

MIT License

##  Author

Samuel Kanyi
DevOps & Cloud Engineering (In Progress)
