# install fabio
```bash
mkdir -p /home/fabio/bin

yum install wget
wget https://github.com/fabiolb/fabio/releases/download/v1.5.9/fabio-1.5.9-go1.10.2-linux_amd64 -O /home/fabio/bin/fabio && chmod +x /home/fabio/bin/fabio
```
# open port 
```bash
firewall-cmd --add-port={8099,8098}/tcp --permanent
firewall-cmd --reload
```
# setup file config
```bash
vi /home/fabio/fabio.properties
vi /usr/lib/systemd/system/fabio.service
```
# limit 
```bash
ulimit -n
ulimit -S -n
ulimit -H -n

echo "
root soft nofile 32000
root hard nofile 64000
" >> /etc/security/limits.d/20-nproc.conf

echo "
session required pam_limits.so
" >> /etc/pam.d/login

yum install util-linux
prlimit --pid 31368 --nofile=32000:64000
```
# check status service
```bash
systemctl restart fabio.service
systemctl status fabio.service
```
