nano /etc/mongod.conf

net:
  port: 27017
  bindIp: 0.0.0.0 // 127.0.0.1 if remove access

sudo systemctl restart mongod

sudo ufw allow 27017

sudo ufw deny 27017

sudo ufw delete allow 27017

// create admin to acess it good ways
mongosh

use admin


db.createUser({
  user: "asadzaman",
  pwd: "pass",
  roles: [{ role: "readWrite", db: "test" }]
})


mongodb://asadzaman:pass@88.222.221.225:27017/test?authSource=admin
