# MyLinuxWiki


## Autologin on Debian console (with no gui):

Edit `/etc/systemd/logind.conf` \
`Change #NAutoVTs=6 to NAutoVTs=1`\
`systemctl edit getty@tty1Create` (to create "/etc/systemd/system/getty@tty1.service.d/override.conf")\
`systemctl edit getty@tty1`

Write:\
`[Service]`\
`ExecStart=`\
`ExecStart=-/sbin/agetty --autologin userName --noclear %I 38400 linux`\

After saving - in terminal:\
`systemctl enable getty@tty1.service`


## Example lsyncd config (/etc/lsyncd/lsyncd.conf.lua) :
>settings {\
>        logfile = "/var/log/lsyncd/lsyncd.log",\
>        statusFile = "/var/log/lsyncd/lsyncd.status",\
>   statusInterval = 20,
>   nodaemon   = false
>}

>sync {\
>        default.rsync,\
>        source = "/home/userName/testSource",\
>        target = "/home/userName/testBackup",\
>delete = "false"\
>}

