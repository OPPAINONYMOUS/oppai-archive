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
tar xf "file name"
```
