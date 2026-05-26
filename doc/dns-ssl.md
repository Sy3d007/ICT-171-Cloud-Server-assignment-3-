# DNS and SSL Configuration

## Domain Registration

Domain `animereviewict171.online` was registered via Namecheap for A$1.39/yr.

## DNS Configuration

Two A records were added in Namecheap Advanced DNS pointing to the server IP:

| Type | Host | Value |
|------|------|-------|
| A Record | @ | 20.213.8.117 |
| A Record | www | 20.213.8.117 |

## SSL/TLS via Let's Encrypt

Install Certbot:

```bash
sudo apt install certbot python3-certbot-apache -y
```

Obtain and deploy SSL certificate:

```bash
sudo certbot --apache -d animereviewict171.online -d www.animereviewict171.online
```

Certificate is saved at `/etc/letsencrypt/live/animereviewict171.online/`
and auto-renews via a scheduled certbot timer.

HTTPS is accessible at `https://animereviewict171.online`
