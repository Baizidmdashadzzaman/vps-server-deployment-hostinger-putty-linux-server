nano /etc/mongod.conf

net:
  port: 27017
  bindIp: 0.0.0.0 // 127.0.0.1 if remove access

sudo systemctl restart mongod

sudo ufw allow 27017

