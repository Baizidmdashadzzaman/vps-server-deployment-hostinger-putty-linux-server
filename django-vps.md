//Virtual environment
python3 -m venv .venv

//Activate
source .venv/bin/activate

//VPS Django Setup
pip install --upgrade pip
pip install -r requirements.txt
python manage.py migrate//not required
python manage.py collectstatic//not required
python manage.py runserver 0.0.0.0:8000//if run for instant existed

//ALLOWED_HOSTS setup
settings.py->
ALLOWED_HOSTS = [
    '88.222.221.225',
    'localhost',
    '127.0.0.1'
]

//Firewall remove
ufw allow 8000
ufw reload
ufw status

//Production Ready
pip install gunicorn
gunicorn Yourtourguide.wsgi:application --bind 0.0.0.0:8000

//systemd service file
nano /etc/systemd/system/yourtour.service->
[Unit]
Description=Yourtour Django App
After=network.target

[Service]
User=root
Group=root
WorkingDirectory=/var/www/Yourtour
ExecStart=/var/www/Yourtour/.venv/bin/gunicorn \
          Yourtourguide.wsgi:application \
          --bind 0.0.0.0:8000
Restart=always

[Install]
WantedBy=multi-user.target

//Enable & Start service
systemctl daemon-reload
systemctl start yourtour
systemctl enable yourtour
systemctl status yourtour

//Restart / Stop command
systemctl restart yourtour
systemctl stop yourtour










