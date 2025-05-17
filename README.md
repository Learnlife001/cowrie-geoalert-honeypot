# 🛡️ Cowrie GeoAlert Honeypot

Real-time honeypot log monitoring, enriched with IP geolocation, live visualizations, and smart alerting via Telegram and Email.

## 📌 What It Does

- **Captures SSH brute-force attempts** using Cowrie Honeypot.
- **Extracts attacker IPs** and enriches them with latitude, longitude, city, and country using MaxMind GeoIP.
- **Pushes logs to Loki** for querying and monitoring.
- **Visualizes attacks live** on a Grafana Geomap dashboard.
- **Sends alert batches** every 10–15 mins to:
  - Your **Telegram bot** (via Bot API)
  - Your **Gmail inbox** (via App Password SMTP)

## 📊 Tech Stack

| Component        | Tool/Tech                        |
|------------------|----------------------------------|
| Honeypot         | Cowrie                           |
| IP Enrichment    | geoip2 + MaxMind GeoLite2        |
| Log Pipeline     | Promtail → Loki → Grafana        |
| Alerting         | Telegram Bot API + SMTP Email    |
| Visualization    | Grafana (Worldmap/Geomap)        |
| Platform         | Ubuntu VM on Microsoft Azure     |

## 📂 Key Scripts

- `cowrie_geo_push.py`: Core script — parses logs, enriches IPs, pushes to Loki, sends alerts.
- `update_attack_map.py`: (Optional) Generates an HTML map view of recent attacks.
- `telegram_alert_log.txt`: Log file of sent Telegram alerts.
- `geo_push.log`: Debug log of IPs sent to Loki.

## ⚙️ Setup Summary

1. 🐍 Create a Python virtual environment.
2. 📦 Install dependencies (`geoip2`, `requests`).
3. 🔐 Configure:
   - `GEO_DB_PATH` to point to `GeoLite2-City.mmdb`
   - `BOT_TOKEN`, `CHAT_ID`, `EMAIL_SENDER`, and `EMAIL_PASS`
4. 🧠 Add cron job:
   ```cron
   */10 * * * * /home/azureuser/geo_env/bin/python3 /home/azureuser/cowrie_geo_push.py >> /home/azureuser/geo_push.log 2>&1
🌍 Grafana Dashboard
Use the job="cowrie_enriched" query to visualize attacker IPs on a live worldmap panel using latitude and longitude extracted in the logs.

🔒 Security Note
No sensitive credentials are stored in version control.

Telegram and Email credentials must be provided via environment variables or secrets management.

🚀 Deployment
This setup was tested and deployed on:

Ubuntu 24.04 Azure VM

Grafana v11+

Cowrie running via systemd

📸 Demo
(You can insert screenshots or attach a sample GIF of your Grafana worldmap panel here.)

📁 License
MIT License — use, modify, and deploy freely.

Built by @Learnlife001

Let me know when you’re ready to copy this into your repo. Want help turning this into your portfolio content too?
