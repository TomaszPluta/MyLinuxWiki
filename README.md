# MyLinuxWiki


## Autologin on Debian console (with no gui):

Edit `/etc/systemd/logind.conf` \
`Change #NAutoVTs=6 to NAutoVTs=1`\
`systemctl edit getty@tty1Create` (to create "/etc/systemd/system/getty@tty1.service.d/override.conf")\
`systemctl edit getty@tty1`

Write:\
`[Service]`\
`ExecStart=`\
`ExecStart=-/sbin/agetty --autologin tomek --noclear %I 38400 linux`\

After saving - in terminal:\
`systemctl enable getty@tty1.service`
