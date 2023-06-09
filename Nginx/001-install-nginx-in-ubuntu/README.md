## install nginx on ubuntu
```sh
apt update
apt install nginx -y
systemctl status nginx
systemctl enable nginx
systemctl reload nginx
ps aux |grep nginx
ls -l /etc/nginx/
```

nginx -t
cat /var/log/nginx/*