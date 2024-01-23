# ufw-ruleset

File: `/etc/ufw/before.rules`

```shell
# Limit to 50 concurrent connections on port 80/443 per IP
-A ufw-before-input -p tcp --syn --dport 80 -m connlimit --connlimit-above 50 -j DROP
-A ufw-before-input -p tcp --syn --dport 443 -m connlimit --connlimit-above 50 -j DROP
# Limit to 100 connections on port 80/443 per 2 seconds per IP
-A ufw-before-input -p tcp --dport 80 -i eth0 -m state --state NEW -m recent --set
-A ufw-before-input -p tcp --dport 80 -i eth0 -m state --state NEW -m recent --update --seconds 2 --hitcount 100 -j DROP
-A ufw-before-input -p tcp --dport 443 -i eth0 -m state --state NEW -m recent --set
-A ufw-before-input -p tcp --dport 443 -i eth0 -m state --state NEW -m recent --update --seconds 2 --hitcount 100 -j DROP
```
