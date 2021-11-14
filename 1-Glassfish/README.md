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

