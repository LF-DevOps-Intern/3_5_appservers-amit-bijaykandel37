QN2

The required packages are installed:
==> Sudo apt install pip
==> Sudo apt install python3
==> Sudo apt install python3-venv

Then a virtual environment is created
==> Python3 -m venv testenv

And the virtual environment is activated:
==> Source testenv/bin/activate

Inside the virtual environment, django and unicorn are installed.
==> Pip install django
==> Pip install gunicorn

To start a django project named server,
==> Django-admin startproject server

Then inside the server project lies a file settings.py. That file is edited to allow hosts:
==> Sudo nano /server/settings.py

And with allowed hosts, we allow our ip as:
ALLOWED_HOSTS = [‘192.168.1.67’]


A file is created for configuration of gunicorn.
For that, we created a directory and inside it a file gunicorn_config.py.
==> Mkdir config
==> Cd config
==> Nano gunicorn_config.py

And inside that file following content is entered:

command = '/home/bj/Desktop/testenv/bin/gunicorn'
pythonpath = '/home/bj/Desktop/server'
bind = '192.168.1.67:8089'
workers = 3


Now we go to the directory containing manage.py and migrate our settings.
==> Python3 manage.py makemigrations
==> Python3 manage.py migrate


We allow our port in firewall as 
==> Sudo ufw allow 8080

Now when we runserver in this port using command:
==> Python3 manage.py runserver 192.168.1.67:8089



On the browser, when we enter the socket address : 192.168.1.67:8089,  we can access the website hosted.






