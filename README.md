# rabbot-web
Contain rabbot.io web and stuff

# To renew SSL
> https://levelup.gitconnected.com/how-to-get-certbot-wildcard-certificates-3d25618a81e0
```bash
# To ensure python will not throw error
export LC_ALL="en_US.UTF-8"
export LC_CTYPE="en_US.UTF-8"
sudo dpkg-reconfigure locales

# Get the source (or pull)
git clone https://github.com/certbot/certbot
cd certbot

# Run certbot auto
sudo ./certbot-auto --os-packages-only

# Clear old stuff
mv /etc/letsencrypt/live/rabbot.io /etc/letsencrypt/live/rabbot.io-`date +%Y-%m-%d`
mv /etc/letsencrypt/archive /etc/letsencrypt/archive-`date +%Y-%m-%d`
mv /etc/letsencrypt/renewal /etc/letsencrypt/renewal-`date +%Y-%m-%d`

# Ask for cert
sudo ./certbot-auto -d rabbot.io -d *.rabbot.io --manual --preferred-challenges dns-01 --server https://acme-v02.api.letsencrypt.org/directory certonly

# Reload
nginx -t && nginx -s reload
```