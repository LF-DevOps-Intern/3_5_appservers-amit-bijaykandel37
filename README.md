QN1
Installation:
==> sudo apt update
==> sudo apt install default-jdk

Then an environment variable is set as:
==> nano /etc/environment
And this part is added to the file :
JAVA_HOME="/usr/lib/jvm/java-11-openjdk-amd64"
==> Source /etc/environment to load the variable.

Then latest Glassfish.zip file is downloaded using command:
==> ‘wget http://download.oracle.com/glassfish/5.0.1/nightly/latest-glassfish.zip’
The file is then extracted
==> Sudo unzip latest-glassfish.zip

The glassfish.service file is created:
==> Sudo nano /etc/systemd/system/glassfish.service

Then the daemon was reloaded and following are commands to start glassfish:
==> sudo systemctl daemon-reload
==> sudo systemctl enable glassfish
==> sudo systemctl start glassfish
==> sudo systemctl status glassfish

After this, we can see the status of glassfish:


After the glassfish server is active, we can access the admin panal with port 4848.

If we go to a browser and enter localhost:4848 then we can see this screen:

To go to the launch the app, we can enter the IP of the VM.
I.e. 192.168.1.191 in our case and default http port for glassfish service is 8080.
So when we go to 192.168.1.191:8080 we can launch the app,


The default HTTP port of the glassfish server is: 8080
And the http port is changed from admin server.
In the left side of admin server, we can see server config:
Inside server-config >NetworkListeners>http-listener-1
We changed the port from 8080 to 8088 and saved the settings.


Now we can access the app from port 8088.



==> Sudo apt install maven
==> wget https://www.apache.org/dist/maven/maven-3/3.6.3/binaries/apache-maven-3.6.3-bin.tar.gz -P /tmp
==> sudo tar xf /tmp/apache-maven-*.tar.gz -C /opt
==> sudo ln -s /opt/apache-maven-3.6.3 /opt/maven

Then maven.sh file is created 
==> Sudo nano /etc/profile.d/maven.sh

And inside this file, this content is appended:

export JAVA_HOME=/usr/lib/jvm/openjdk-11-amd64
export M2_HOME=/opt/maven
export MAVEN_HOME=/opt/maven
export PATH=${M2_HOME}/bin:${PATH}


==> sudo chmod +x /etc/profile.d/maven.sh
==> source /etc/profile.d/maven.sh #environment-variables are loaded

To create war file:
==> Mvn archetype:generate


Then go to dir containing pom.xml file and enter
==> Mvn validate
==> Mvn compile
==> Mvn package
==> Mvn clean install

This creates a war file which is then selected from admin server page and launched and deployed.




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

