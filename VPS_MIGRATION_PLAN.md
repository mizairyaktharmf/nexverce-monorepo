# Nexverce — VPS Migration Plan

> Status: **Pending Execution**
> Prepared: April 2026
> Author: Mizairy Akthar (NexCode Nova)

---

## Overview

Moving the entire Nexverce project from Render + Vercel free tiers to a self-managed VPS.
Benefits: no cold starts, full control, all subdomains on one server, predictable cost.

---

## Apps Being Migrated

| App | Type | Current Host | Target on VPS |
|---|---|---|---|
| `nexverce-backend` | Node.js / Express + Socket.io | Render | PM2 process |
| `nexverce-client` | React / Vite (main website) | Vercel / Render | Nginx static |
| `nexverce-admin` | React / Vite (admin panel) | Render | Nginx static |
| `nexverce-vendor` | React / Vite (vendor portal) | Vercel | Nginx static |
| MongoDB | Database | **Atlas (cloud)** | **Stays on Atlas — do NOT self-host** |

---

## Recommended VPS Size

### Starter (0 – 10,000 monthly visits)
**1 vCPU / 2 GB RAM / 50 GB SSD — ~$12/month**

| Resource | Reason |
|---|---|
| 2 GB RAM | Node.js ~200–300 MB + Nginx ~50 MB + OS ~400 MB = comfortable fit |
| 1 vCPU | Sufficient for API + static serving at low traffic |
| 50 GB SSD | OS ~10 GB + apps + node_modules ~3 GB + logs ~2 GB = plenty of headroom |

### Growth (10,000 – 50,000 monthly visits)
**2 vCPU / 4 GB RAM / 80 GB SSD — ~$24/month**

### Minimum Budget (under 3,000 visits/mo)
**1 vCPU / 1 GB RAM / 25 GB SSD — ~$6/month** *(may need swap enabled)*

---

## Target Architecture

```
Internet
   |
Nginx (ports 80 + 443)   <-- SSL via Let's Encrypt (free, auto-renews)
   |
   +-- nexverce.com           --> /var/www/nexverce-client/dist   (static files)
   +-- admin.nexverce.com     --> /var/www/nexverce-admin/dist    (static files)
   +-- vendor.nexverce.com    --> /var/www/nexverce-vendor/dist   (static files)
   +-- api.nexverce.com       --> localhost:5000  (Node.js via PM2)
```

---

## Step-by-Step Execution Guide

### Step 1 — Provision the VPS
1. Purchase VPS (Ubuntu 22.04 LTS recommended)
2. Note the public IP address
3. SSH into server: `ssh root@<VPS_IP>`

### Step 2 — Initial Server Setup
```bash
# Update system
apt update && apt upgrade -y

# Install Node.js 18
curl -fsSL https://deb.nodesource.com/setup_18.x | bash -
apt install -y nodejs

# Install Nginx
apt install -y nginx

# Install PM2 (process manager for Node.js)
npm install -g pm2

# Install Certbot (free SSL)
apt install -y certbot python3-certbot-nginx

# Configure firewall
ufw allow OpenSSH
ufw allow 'Nginx Full'
ufw enable
```

### Step 3 — Deploy the Backend
```bash
# Clone backend repo
cd /var/www
git clone https://github.com/mizairyaktharmf/Nexverce-Backend.git nexverce-backend
cd nexverce-backend

# Install production dependencies only
npm install --production

# Create .env file (copy your local .env contents here)
nano .env
# Paste all env vars — update these two:
#   BACKEND_URL=https://api.nexverce.com
#   FRONTEND_URL=https://nexverce.com
#   LINKEDIN_REDIRECT_URI=https://api.nexverce.com/api/linkedin/callback

# Start with PM2
pm2 start server.js --name nexverce-backend

# Auto-restart on server reboot
pm2 save
pm2 startup
# (run the command it outputs)
```

### Step 4 — Build & Deploy Frontend Apps
```bash
# On your LOCAL machine, build each app:
cd nexverce-client  && npm install && npm run build
cd nexverce-admin   && npm install && npm run build
cd nexverce-vendor  && npm install && npm run build

# Upload dist/ folders to VPS (run from local terminal):
scp -r nexverce-client/dist  root@<VPS_IP>:/var/www/nexverce-client/
scp -r nexverce-admin/dist   root@<VPS_IP>:/var/www/nexverce-admin/
scp -r nexverce-vendor/dist  root@<VPS_IP>:/var/www/nexverce-vendor/
```

### Step 5 — Configure Nginx
```bash
# On VPS, create Nginx config:
nano /etc/nginx/sites-available/nexverce
```

Paste this config:
```nginx
# ── Main Website ──────────────────────────────────────────────
server {
    server_name nexverce.com www.nexverce.com;
    root /var/www/nexverce-client/dist;
    index index.html;
    location / {
        try_files $uri /index.html;
    }
}

# ── Admin Panel ───────────────────────────────────────────────
server {
    server_name admin.nexverce.com;
    root /var/www/nexverce-admin/dist;
    index index.html;
    location / {
        try_files $uri /index.html;
    }
}

# ── Vendor Portal ─────────────────────────────────────────────
server {
    server_name vendor.nexverce.com;
    root /var/www/nexverce-vendor/dist;
    index index.html;
    location / {
        try_files $uri /index.html;
    }
}

# ── Backend API ───────────────────────────────────────────────
server {
    server_name api.nexverce.com;
    location / {
        proxy_pass http://localhost:5000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```

```bash
# Enable the config
ln -s /etc/nginx/sites-available/nexverce /etc/nginx/sites-enabled/
nginx -t        # test for errors
systemctl reload nginx
```

### Step 6 — Point DNS to VPS
In your domain registrar (or Cloudflare), add these A records:

| Record | Name | Value |
|---|---|---|
| A | `@` (nexverce.com) | `<VPS IP>` |
| A | `www` | `<VPS IP>` |
| A | `api` | `<VPS IP>` |
| A | `admin` | `<VPS IP>` |
| A | `vendor` | `<VPS IP>` |

Wait 5–30 minutes for DNS to propagate.

### Step 7 — Install SSL (Free HTTPS)
```bash
certbot --nginx \
  -d nexverce.com \
  -d www.nexverce.com \
  -d api.nexverce.com \
  -d admin.nexverce.com \
  -d vendor.nexverce.com
```
Certbot auto-renews every 90 days. Nothing else needed.

---

## What Does NOT Change

| Item | Action |
|---|---|
| MongoDB Atlas | Keep as-is, just keep MONGO_URI in .env |
| Resend API (emails) | Keep as-is, just keep RESEND_API_KEY in .env |
| OpenAI API | Keep as-is, just keep OPENAI_API_KEY in .env |
| LinkedIn OAuth | Only update redirect URI to `https://api.nexverce.com/api/linkedin/callback` |

---

## Monthly Cost After Migration

| Item | Cost |
|---|---|
| VPS (2 GB RAM starter) | ~$12/mo |
| Domain (nexverce.com) | Already owned |
| SSL Certificates | Free (Let's Encrypt) |
| MongoDB Atlas | Free tier |
| Resend Email | Free (3,000 emails/mo) |
| **Total** | **~$12/month** |

---

## Post-Migration Checklist

- [ ] `https://nexverce.com` loads the main website
- [ ] `https://vendor.nexverce.com` loads vendor portal, login works
- [ ] `https://admin.nexverce.com` loads admin panel
- [ ] `https://api.nexverce.com/api/vendors` returns JSON (not 502 error)
- [ ] Vendor registration sends verification email
- [ ] Socket.io works (notifications appear in vendor dashboard)
- [ ] `pm2 status` shows `nexverce-backend` as **online**
- [ ] Server auto-restarts backend after reboot (`pm2 startup`)
- [ ] SSL padlock shows on all 4 domains

---

## Future Scaling (When Needed)

- Resize VPS to 4 GB RAM at ~$24/mo when traffic grows past 10k/mo
- Add Cloudflare in front for free CDN + DDoS protection (just proxy DNS through Cloudflare)
- Set up GitHub Actions for auto-deploy on push (CI/CD)
- Consider moving MongoDB to a dedicated cluster if data grows past 512 MB free tier
