### Install AdGuard Home Public Server
```
curl -s -S -L https://raw.githubusercontent.com/AdguardTeam/AdGuardHome/master/scripts/install.sh | sh -s -- -v
```
### Install Lego - LetsEncrypt Client
```
cd /tmp
```
```
curl -Ls https://api.github.com/repos/xenolf/lego/releases/latest | grep browser_download_url | grep linux_amd64 | cut -d '"' -f 4 | wget -i -
```
```
tar xf file_name
```
```
sudo mkdir -p /opt/certs/letsencrypt
```
```
sudo mv lego /opt/certs/letsencrypt/lego
```
### Create A Cloudflare API Key Or Token
First, you need to create an API key that has ‘Read‘ access to the zone of your domain and permission to ‘Edit‘ DNS in Cloudflare. API Tokens use the standard Authorization.

To create your API Token go to the ‘API Tokens’ section of your user profile which can be found at https://dash.cloudflare.com/profile/api-tokens
![b](https://raw.githubusercontent.com/OPPAINONYMOUS/oppai-archive/main/Install_AdGuard_DoH/%231.png)



