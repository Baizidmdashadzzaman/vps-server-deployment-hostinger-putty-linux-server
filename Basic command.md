#### Basic command list

Show file including env

```bash
 cd -alh
```

creat or edit file

```bash
 nano .env
```

///////////////////////////////////////////////
If close putty server will off, for this solution use pm2

```bash
 npm install -g pm2
```

```bash
 pm2 start app.js --name "your-app-name"
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

///////////////////////////////////////////////