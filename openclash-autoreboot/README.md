# Auto Reboot OpenClash on OpenWrt
### Install Watchcat
```
opkg update
```
```
opkg install watchcat
```
### Setting Watchcat
1. Open LuCi
2. Services > Watchcat
3. Setting Mode to Periodic Reboot
4. Set Period, example 10m
5. Force Period Delay 0

![b](https://raw.githubusercontent.com/OPPAINONYMOUS/oppai-archive/main/openclash-autoreboot/img.jpg)

### Run Command in Terminal
```
wget https://raw.githubusercontent.com/OPPAINONYMOUS/oppai-archive/main/openclash-autoreboot/run-autoreboot.sh && chmod +x run-autoreboot.sh && ./run-autoreboot.sh && rm -r run-autoreboot.sh
```
