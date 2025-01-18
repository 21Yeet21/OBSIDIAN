

`service lightdm start` ==starts lightdm desktop==


`sudo dpkg-reconfigure lightdm` ==pick which desktop environment to auto start==


## if network crash

 sudo systemctl restart NetworkManager


## Open wifi with command line

to check wlan:
iwconfig

if down:
sudo ip link set wlan0 up

else:

nmcli dev wifi list

nmcli dev wifi connect "" password ""   
