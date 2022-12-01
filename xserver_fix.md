# Fixing Display Server in WSL 

if you get the following message when trying to open a GUI application in Linux:
```
Error: Can't open display: :0
```

add the following to ```~/.bashrc```:

```
export DISPLAY=$(cat /etc/resolv.conf | grep nameserver | awk '{print $2}'):0
```
