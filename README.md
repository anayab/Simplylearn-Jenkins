# Simplylearn-Jenkins
How to install Jenkins:
```
Step 1 — Installing Jenkins
The version of Jenkins included with the default Ubuntu packages is often behind the latest available version from the project itself. To ensure you have the latest fixes and features, use the project-maintained packages to install Jenkins.

First, add the repository key to your system:

wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key |sudo gpg --dearmor -o /usr/share/keyrings/jenkins.gpg
The gpg --dearmor command is used to convert the key into a format that apt recognizes.

Next, let’s append the Debian package repository address to the server’s sources.list:

sudo sh -c 'echo deb [signed-by=/usr/share/keyrings/jenkins.gpg] http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
The [signed-by=/usr/share/keyrings/jenkins.gpg] portion of the line ensures that apt will verify files in the repository using the GPG key that you just downloaded.

After both commands have been entered, run apt update so that apt will use the new repository.

sudo apt update
Finally, install Jenkins and its dependencies:

sudo apt install jenkins
Now that Jenkins and its dependencies are in place, we’ll start the Jenkins server.

Step 2 — Starting Jenkins
now that Jenkins is installed, start it by using systemctl:

sudo systemctl start jenkins.service
Since systemctl doesn’t display status output, we’ll use the status command to verify that Jenkins started successfully:

sudo systemctl status jenkins
If everything went well, the beginning of the status output shows that the service is active and configured to start at boot:

Output
● jenkins.service - Jenkins Continuous Integration Server
     Loaded: loaded (/lib/systemd/system/jenkins.service; enabled; vendor preset: enabled)
     Active: active (running) since Mon 2022-04-18 16:07:28 UTC; 2min 3s ago
   Main PID: 88180 (java)
      Tasks: 42 (limit: 4665)
     Memory: 1.1G
        CPU: 46.997s
     CGroup: /system.slice/jenkins.service
             └─88180 /usr/bin/java -Djava.awt.headless=true -jar /usr/share/java/jenkins.war --webroot=/var/cache/jenkins/war --httpPort=8080

Now that Jenkins is up and running, adjust your firewall rules so that you can reach it from a web browser to complete the initial setup.

Step 3 — Opening the Firewall
To set up a UFW firewall, visit Initial Server Setup with Ubuntu 22.04, Step 4- Setting up a Basic Firewall. By default, Jenkins runs on port 8080. Open that port using ufw:

sudo ufw allow 8080
Note: If the firewall is inactive, the following commands will allow OpenSSH and enable the firewall:

sudo ufw allow OpenSSH
sudo ufw enable
Check ufw’s status to confirm the new rules:

sudo ufw status
You’ll notice that traffic is allowed to port 8080 from anywhere:

Output
Status: active

To                         Action      From
--                         ------      ----
OpenSSH                    ALLOW       Anywhere
8080                       ALLOW       Anywhere
OpenSSH (v6)               ALLOW       Anywhere (v6)
8080 (v6)                  ALLOW       Anywhere (v6)
With Jenkins installed and a firewall configured, you have completed the installation stage and can continue with configuring Jenkins.

Step 4 — Setting Up Jenkins
To set up your installation, visit Jenkins on its default port, 8080, using your server domain name or IP address: http://your_server_ip_or_domain:8080
```

## REFERENCES:
https://www.digitalocean.com/community/tutorials/how-to-install-jenkins-on-ubuntu-22-04
