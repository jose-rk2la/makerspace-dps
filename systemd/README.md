# How to enable systemd in WSL Ubuntu-18.04 #

You may get this error in command line when trying to run a service with WSL:  

```
System has not been booted with systemd as init system (PID 1). Can't operate.
```  

Some services need to be initiated with ```systemd``` via ```systemctl``` but ```systemd``` is not natively supported in WSL. Follow these steps to enable it:  

1. Upgrade to WSL 2 if you are on WSL 1 by downloading this package on your Windows machine and running it:  https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi
2. Set WSL 2 as the default for Ubuntu 18.04 by opening Powershell in Windows and running:  
```
wsl --set-version Ubuntu-18.04 2
```
3. Go into wsl with ```wsl -u root -d Ubuntu-18.04``` in Powershell; make sure you have git installed then clone the following repo and run the shell command:  
```
sudo apt install git
git clone https://github.com/DamionGans/ubuntu-wsl2-systemd-script.git
cd ubuntu-wsl2-systemd-script/
bash ubuntu-wsl2-systemd-script.sh
bash ubuntu-wsl2-systemd-script.sh --force
``` 
4. Exit WSL with ```exit``` and run the following in Powershell to restart WSL:  
```
wsl --shutdown -d Ubuntu-18.04
wsl -u root -d Ubuntu-18.04
```
5. You should now be able to run ```systemctl``` commands natively in WSL Ubuntu.