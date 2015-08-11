# dahdi-install-helper
How to install asterisk with dahdi driver
####Step 1:Download Denpendency
#####1.libpri
Get file from asterisk official site
```
$sudo make 
$sudo make install
```
#####2.libss7--ss7 singal
```
$sudo apt-get install libss7-1 libss7-dev libss7-dbg
```
####Step 2:install dahdi 
##### 1. install dahdi-tools
```bash
$sudo apt-get install libnewt-dev
$sudo apt-get install libncurses5-dev
$sudo apt-get install libtonezone-dev
$sudo apt-get install fxload
$cd tools
$./configure
$make 
```

#####2.install dahdi
```
$cd .. 
$make && make install
```
#####3.asterisk 


```
$sudo apt-get install libncurses-dev libz-dev libssl-dev libxml2-dev libsqlite3-dev libnewt-dev
$./configure 
$make menuselect (check chan_dahdi!!!)
$make 
$make install

```

####Step 3:configure dahdi and asterisk
#####1.open dahdi.blocklist file 
```
sudo vim /etc/modprobe.d/dahdi.blocklist
```
#####2.delete or comment out wcte11xp in blocklist and add netjet module to blocklist

```
blacklist netjet /* add this line or delete the first '#' character
#blacklist wctellxp /*comment out*/
```
 
#####3.reboot and start all of it
```
$sudo reboot now
$sudo modprobe dahdi  ; load dahdi driver
$sudo modprobe wcte11xp opermode=YOUR　COUNTRY; load the wctdm driver with your country 
$sudo dahdi_genconf  ;Generate configure files
$sudo dahdi_cfg –vvvv ; start channels
$sudo asterisk -rx "core restart now"
```
or
```
asterisk -rx "core restart now"
```
#####4.check dahdi is ok
```
$lsdahdi
```
####Troubleshooting

check /etc/asterisk/chan_dahdi.conf  

```[channels]
\#include  /etc/asterisk/dahdi-channels.conf
```
