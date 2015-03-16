# dahdi-install-helper
How to install asterisk with dahdi driver easily
####Step 1:Download Denpendency
#####1.libpri
Get file from asterisk official site
```
$make 
$make install
```
#####2.libss7--ss7 singal
```
$apt-get libss7-1 libss7-dev libss7-dbg
```
#####3.opennr2--MFC/R2 (telephony) call setup library
```
$apt-get libopenr2-3 libopenr2-bin libopenr2-dev
```
####Step 2:install dahdi and asterisk
#####1.dahdi
get lastest dahdi
```
$make && make install
```
#####2.asterisk 
```
$./configure 
$make menuselect (check chan_dahdi!!!)
$make 
$make install
```

####Step 3:configure dahdi and asterisk
#####1.comment out  wcte11xp in blocklist
```
/etc/modprobe.d/dahdi.blacklist
```
#####2.start all of it
```
$modprobe dahdi  ; load dahdi driver
$modprobe wcte11xp opermode=YOUR　COUNTRY; load the wctdm driver with your country 
$dahdi_genconf  ;Generate configure files
$dahdi_cfg –vvvv ; start channels
$asterisk -rx "core restart now"
```
or
```
service dahdi start
asterisk -rx "core restart now"
```
#####3.check dahdi is ok
```
$lsdahdi
```
####Troubleshooting

check /etc/asterisk/chan_dahdi.conf
[channels]
\#include  /etc/asterisk/dahdi-channels.conf
