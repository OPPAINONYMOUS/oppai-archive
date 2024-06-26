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

There are two ways to create your token – You can either create it from scratch through the “Create Custom Token” option or you can start with a predefined template, by selecting “Use template”, here, in this case, we will use the “Edit zone DNS” template to create an API Token that can edit a single zone’s DNS records.
![b](https://raw.githubusercontent.com/OPPAINONYMOUS/oppai-archive/main/Install_AdGuard_DoH/%232.png)

once the template is selected, you need to pick a zone for the API token.
Notice that the DNS Edit permission was already pre-selected. Enter a token descriptive name, then add one more permission-giving zone Read access as shown in the figure below.
![b](https://raw.githubusercontent.com/OPPAINONYMOUS/oppai-archive/main/Install_AdGuard_DoH/%233.png)

Once you select “Continue to the summary”, you are given a chance to review the selection.

Here, the resources and permissions are quite simple, but this gives you a chance to make sure you are giving the API Token exactly the correct amount of privilege before creating it.

Once created, you are presented with the API Token. This screen is the only time you will be presented with the secret so be sure to put the secret in a safe place!

Anyone with this secret can perform the granted actions on the resources specified to protect it like a password.

In the below screenshot, we have black-box the secret for obvious reasons. If you happen to lose the secret, you can always regenerate it from the API Tokens table so you don’t have to configure all the permission again.
![b](https://raw.githubusercontent.com/OPPAINONYMOUS/oppai-archive/main/Install_AdGuard_DoH/%234.png)

In addition to the secret itself, this page provides an example curl request that can be used to verify that the token was successfully created

### Generate A Let’s Encrypt Certificate
Please remember to replace your CLOUDFLARE_AND_API_TOKEN value, the Domain placeholder with your actual domain name, and the Email-Address placeholder with your email address.
```
cd /opt/certs/letsencrypt/
```
```
sudo CLOUDFLARE_DNS_API_TOKEN=Your-token-number ./lego --dns cloudflare --domains your-domain-name  --email admin@example.com --path="/opt/certs/letsencrypt" run
```
EXAMPLE :
```
sudo CLOUDFLARE_DNS_API_TOKEN=ELQByDJc2Gx82P8wUkAd-Ro-xD4HddoPW8nuI_dH ./lego --dns cloudflare --domains doh.oppaivpn.my.id  --email e.periantara@gmail.com --path="/opt/certs/letsencrypt" run
```
### Auto Renew Certs
```
sudo mkdir -p /opt/certs/letsencrypt/scripts
```
```
sudo nano /opt/certs/letsencrypt/scripts/renew-certificate.sh
```
nano editor will open the file, enter the following content into the script and save it depending on if you have Apache and Nginx.

Please remember to replace your CLOUDFLARE_AND_API_TOKEN value, the Domain placeholder with your actual domain name, and the Email-Address placeholder with your email address.

For Apache :
```
#!/bin/bash
 
cd /opt/certs/letsencrypt/
 
sudo CLOUDFLARE_DNS_API_TOKEN=Your API Token ./lego --dns cloudflare --domains domain.com --email admin@webkul.com --path="/opt/certs/letsencrypt" renew --days 90
 
sudo systemctl restart apache2
```

For Nginx :
```
#!/bin/bash
 
cd /opt/certs/letsencrypt/
 
sudo CLOUDFLARE_DNS_API_TOKEN=Your API Token ./lego --dns cloudflare --domains domain.com --email admin@webkul.com --path="/opt/certs/letsencrypt" renew --days 90
 
sudo systemctl restart nginx
```
EXAMPLE For Nginx :
```
#!/bin/bash

cd /opt/bitnami/letsencrypt/

sudo CLOUDFLARE_DNS_API_TOKEN=ELQByDJc2Gx82P8wUkAd-Ro-xD4HddoPW8nuI_dH ./lego --dns cloudflare --domains doh.oppaivpn.my.id  --email e.periantara@gmail.com --path="/opt/certs/letsencrypt" renew --days 90

sudo systemctl restart nginx
```
Then press Ctrl+X to save the script and exit the nano editor.

Next, you need to make the script executable using the following command.
```
sudo chmod +x /opt/certs/letsencrypt/scripts/renew-certificate.sh
```
```
sudo crontab -e
```
Finally, add the below line lines to the crontab file and then press Ctrl + X to save it and exit the nano editor.
```
0 0 * * * bash /opt/certs/letsencrypt/scripts/renew-certificate.sh 2> /dev/null
```
