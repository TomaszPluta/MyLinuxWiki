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


## Turn off external usb-disk:
`udisksctl power-off -b /dev/sdb` - need to re-plug to operate again\
or:\
`sudo hdparm -S 1 /dev/sdb` - suspend after 5sec inactivity (back to operation after any access, eg. remount)


## Simplest mount operation:
`sudo mount -t ntfs /dev/sdxN /mounting/point/here`

## Mount network samba share
`sudo mount -t cifs -o credentials=/home/user/SmbCredentialFileName,iocharset=utf8,rw,nodfs,_netdev,noperm //10.0.0.x/ShareName/ /mount/point/here/` 

credential file example:
> user=UserNameHere\
> password=UserPasswordHere\
> domain=WorkgroupNameHere (default:WORKGROUP)
> 

## samba  network samba share
>/etc/samba/smb.conf\
>[global]\
>   server string = MyServerName\
>   workgroup = WorkgroupNameHere (default:WORKGROUP)\
>   \
>[MyShareName]\
>        path = /path/to/shared/dir\
>        browseable = yes\
>        read only = no\
>        force create mode = 0660\
>        force directory mode = 2770\
>        valid users = userName\
