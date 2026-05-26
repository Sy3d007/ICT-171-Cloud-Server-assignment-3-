# Server Status Script

## Overview

This script generates a live server health status page and saves it as an HTML file accessible on the web. It runs automatically every hour via a cron job, providing an always up to date view of the server's health.

The output is publicly visible at: `https://animereviewict171.online/server-status.html`

## Script

```bash
#!/bin/bash

# Server Status Script for Anime Reviews ICT171
# This script checks server health and logs the output to a web-accessible file
# Author: Your Name - Student ID: 35932261

OUTPUT="/var/www/html/wordpress/server-status.html"

cat > "$OUTPUT" << EOF
<!DOCTYPE html>
<html>
<head>
    <title>Server Status - Anime Reviews ICT171</title>
    <style>
        body { font-family: Arial, sans-serif; max-width: 800px; margin: 40px auto; padding: 20px; background: #1a1a2e; color: #eee; }
        h1 { color: #e94560; }
        .stat { background: #16213e; padding: 15px; margin: 10px 0; border-radius: 8px; border-left: 4px solid #e94560; }
        .label { color: #e94560; font-weight: bold; }
    </style>
</head>
<body>
    <h1>Server Status - Anime Reviews ICT171</h1>
    <p>Last updated: $(date)</p>
    <div class="stat"><span class="label">Hostname:</span> $(hostname)</div>
    <div class="stat"><span class="label">Uptime:</span> $(uptime -p)</div>
    <div class="stat"><span class="label">Disk Usage:</span> $(df -h / | awk 'NR==2 {print $3 " used of " $2 " (" $5 " full)"}')</div>
    <div class="stat"><span class="label">Memory Usage:</span> $(free -h | awk 'NR==2 {print $3 " used of " $2}')</div>
    <div class="stat"><span class="label">Apache Status:</span> $(systemctl is-active apache2)</div>
    <div class="stat"><span class="label">MySQL Status:</span> $(systemctl is-active mysql)</div>
</body>
</html>
EOF

echo "Server status updated at $(date)"
```

## How to Run

Make the script executable:

```bash
chmod +x /home/azureuser/server-status.sh
```

Run manually:

```bash
sudo bash /home/azureuser/server-status.sh
```

## Automated Execution

The script runs automatically every hour via cron:

```bash
(crontab -l 2>/dev/null; echo "0 * * * * sudo bash /home/azureuser/server-status.sh") | crontab -
```

## Verifiable Output

The script output is publicly accessible at:
`https://animereviewict171.online/server-status.html`

The page shows live server stats including hostname, uptime, disk usage, memory usage, and service status for Apache and MySQL.
