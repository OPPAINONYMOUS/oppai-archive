### LINK INSTALL AdGuard Home Public Server
```
curl -s -S -L https://raw.githubusercontent.com/AdguardTeam/AdGuardHome/master/scripts/install.sh | sh -s -- -v
```
### Command Restore Backup
```
cd /opt
```
```
wget https://raw.githubusercontent.com/OPPAINONYMOUS/oppai-archive/main/Backup_Adguard_DoH/backup_config_DoH.zip
```
```
unzip backup_config_DoH.zip
```
```
rm -f backup_config_DoH.zip
```
```
sudo chmod +x /opt/certs/letsencrypt/scripts/renew-certificate.sh
```
```
sudo crontab -e
```
```
0 0 1 * * bash /opt/certs/letsencrypt/scripts/renew-certificate.sh 2> /dev/null
```
