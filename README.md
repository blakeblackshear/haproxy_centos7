# HAProxy in CentOS 7 with certificates on a mounted directory

HAProxy fails to load SSL certificates that are stored on a mounted directory
when it is started by systemd in CentOS 7.

The following errors occur when running `vagrant up`:
```
Jun 25 21:49:04 localhost.localdomain haproxy-systemd-wrapper[24315]: 
  [ALERT] 175/214904 (24316) : parsing [/etc/haproxy/haproxy.cfg:22] : 'bind *:443' : 
  unable to load SSL private key from PEM file '/etc/ssl/private_tmpfs/private.pem'.
```

If you comment out the following line in the vagrantfile, haproxy starts fine:
```
sudo mount -t tmpfs -o size=20m tmpfs /etc/ssl/private_tmpfs
```

I have tried this with `ramfs` and mounting an additional device.
