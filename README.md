# 🚀 Telegram Bot Deployment Guide (Node.js + VPS)

This guide explains how to deploy your Node.js Telegram bot on any **VPS (HostGraber, Contabo, Hetzner, etc.)**.

---

## 🧠 Requirements
- A VPS with **root** access (e.g., `160.187.xx.xx`)
- **Node.js 18+**
- **Git**
- **PM2** (for 24/7 uptime)
- Your **Telegram Bot Token** from [@BotFather](https://t.me/BotFather)

---

## ⚙️ 1. Connect to VPS

```bash
ssh root@YOUR_SERVER_IP

---
## 🧩 2. Update & Install Essentials

🟡 For Ubuntu / Debian:
sudo apt update && sudo apt upgrade -y
sudo apt install -y curl git
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt install -y nodejs

🔵 For CentOS / AlmaLinux / RockyLinux:
dnf update -y
dnf install -y curl git
curl -fsSL https://rpm.nodesource.com/setup_20.x | bash -
dnf install -y nodejs


Check versions:
node -v
npm -v

📦 3. Clone the Repository

cd /root
git clone https://github.com/YOUR_GITHUB_USERNAME/YOUR_BOT_REPO.git
cd YOUR_BOT_REPO


🔐 4. Create Environment File

nano .env

Example:
BOT_TOKEN=123456:ABCDEF-your-bot-token
MONGO_URL=mongodb+srv://your-db-url
OWNER_ID=123456789

Save → CTRL + X, Y, then Enter.

📚 5. Install Dependencies

npm install

🧪 6. Test the Bot

 node bot.js / node index.js

🚀 7. Run the Bot 24/7 with PM2

npm install -g pm2
pm2 start bot.js --name "yourbotname"
pm2 save
pm2 startup


View running bots:
pm2 list


View logs:
pm2 logs yourbotname

Restart bot:
pm2 restart yourbotname

Stop bot:
pm2 stop yourbotname

🔄 8. Update the Bot Later

When you push new updates to GitHub:

cd /root/YOUR_BOT_REPO
git pull
pm2 restart yourbotname

🔒 9. (Optional) Secure Your VPS

dnf install -y fail2ban
systemctl enable --now fail2ban


