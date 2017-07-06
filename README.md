## IP Address & SSH port
Public IP: 13.59.188.21

| Application | Protocol | Port range
| ------------|----------|-------
| SSH         | TCP      | 220
| HTTP        | TCP      | 80

## URL
- [http://ec2-13-59-188-21.us-east-2.compute.amazonaws.com](http://ec2-13-59-188-21.us-east-2.compute.amazonaws.com/courses/)

## Configuration
1. update/upgrade all packages
- `sudo apt-get update`
- `sudo apt-get upgrade`
2. Change the SSH port from 22 to 2200
- `sudo vim /etc/ssh/sshd_config`
- change the port 22 to port 2200
- restart the server by running  `sudo service sshd restart`
3. Configure the Uncomplicated Firewall (UFW) to only allow incoming connections for SSH (port 2200), HTTP (port 80), and NTP (port 123)
- `sudo ufw allow 2200/tcp`
- `sudo ufw allow 80/tcp`
- `sudo ufw allow 123/udp`
- `sudo ufw enable`
4. Create a new user account named grade
- `sudo adduser grader`
5. Give grader the permission to sudo
- `sudo touch /etc/sudoers.d/grader`
- `sudo nano /etc/sudoers.d/grader` and type in `grader ALL=(ALL:ALL) ALL` 
6. Create an SSH key pair for grader using the ssh-keygen tool and copy the public key to the ubuntu development environment.
- generate keys on local machine using `ssh-keygen` in `~/.ssh`
- `$su - grader`  
- `$mkdir .ssh`
- `$touch .ssh/authorized_keys`
- and then copy and paste the public key to the authorized_keys file.
7. Configure the local timezone to UTC.
- `sudo dpkg-reconfigure tzdata`
- select UTC
8. Install and configure Apache to serve a Python mod_wsgi application.
- install apache2 `sudo apt-get install apache2`
- install mod-wsgi `sudo apt-get install python-setuptools libapache2-mod-wsgi
- `sudo service apache2 restart`
9. Install and configure PostgreSQL
- Install PostgreSQL `sudo apt-get install postgresql`
- Check if no remote connections are allowed `sudo vim /etc/postgresql/9.3/main/pg_hba.conf`
- login as a postgres `sudo su - postgres`
- `psql`
- Create a new database named catalog and create a new user named catalog in postgreSQL shell
- `postgres=# CREATE DATABASE catalog;`
- `postgres=# CREATE USER catalog;`
- `postgres=# ALTER ROLE catalog WITH PASSWORD 'password';
- Give user "catalog" permission to create db
- `ALTER USER catalog CREATEDB;`
- `CREATE DATABASE catalog WITH OWNER catalog;`
10. Clone and setup your project
- helpful link : [here](https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps)


## Flashcard App
This Flask application help people to create collective flashcards and learn things efficiently. Users can create courses and participates in creating more flashcards to every courses. Also, users can collect the memorized cards and learn. This application should be updated to add more functionality. Inviting for study, and user ability to put equations pictures should be added to increase the usability of this app.

## Third-Party Components
- Flask
- PostgreSQL
- SQLAlchemy
- oauth2client
- Google Sign-In
- Bootstrap
