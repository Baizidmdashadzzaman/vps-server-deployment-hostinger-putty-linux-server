#### Basic command list

Show file including env

```bash
 cd -alh
```

////////////////////////////////////
creat or edit file

```bash
 nano .env
```
clt x -> Y -> Enter
///////////////////////////////////

///////////////////////////////////////////////
If close putty server will off, for this solution use pm2

```bash
 npm install -g pm2
```

```bash
 pm2 start app.js --name "your-app-name"
```
```bash
 pm2 start npm --name "vue-dev-server" -- run dev
 pm2 start npm --name "react-dev-server" -- run start
 pm2 start npm --name "Run Web" -- run dev
 pm2 start src/index.js --name "Run Admin"
 pm2 start serve --name "Run Admin"
 pm2 start serve --name "Run Admin" -- -s build -p 4000
 pm2 start /usr/bin/serve --name "Run Admin" -- -s build -p 4000
```

optional::

Save the Process List (Optional): To ensure the application restarts after a server reboot:

```bash
 pm2 save
```

Enable Startup Script: Generate a startup script to automatically restart pm2 processes on server boot:

```bash
 pm2 startup
```

Check Running Applications:

```bash
 pm2 list
```

Stop Running Applications:

```bash
 pm2 stop "Run Admin"
```

```bash
 pm2 delete "Run Admin"
```

///////////////////////////////////////////////

Allow legacy in node js:
```bash
  export NODE_OPTIONS=--openssl-legacy-provider
```