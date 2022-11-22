---
title: Getting Started With XAMPP
date: 2020-03-13 09:00:00
tags:
  - Web Development
category: tech
keywords:
  - Web Development
  - Web Server
  - XAMPP
  - Apache
  - PHP
  - MySQL
  - FTP
  - FileZilla
mathjax: true
---

## What is XAMPP?

XAMPP is a free and open-source cross-platform web server solution stack package developed by Apache Friends, consisting mainly of the Apache HTTP Server, MariaDB database, and interpreters for scripts written in the PHP and Perl programming languages. XAMPP is easy to install and to use - just download, extract and start. XAMPP is a completely free, easy to install Apache distribution containing MariaDB, PHP, and Perl. The XAMPP open source package has been set up to be incredibly easy to install and to use.

## Installing XAMPP

- Download the latest version of XAMPP from [https://www.apachefriends.org/download.html](https://www.apachefriends.org/download.html)
- Install it, ignore the UAC first. Decide where your XAMPP folder will be created. In my case I have an allocated drive for all my development applications and I never put it in drive C.
- Start the Apache and MySQL service.
- Open the browser and go to [http://localhost](http://localhost) or [http://ip-address](http://ip-address) if you are accessing it from another computer.

## Configuring Apache, PHP and MySQL

### Accessing phpMyadmin over the network

By default you will get the following error when accessing the phpMyadmin over network in after installing XAMPP.

```console
    Access forbidden!
    New XAMPP security concept:
    Access to the requested directory is only available from the local network.
    This setting can be configured in the file "httpd-xampp.conf".
    If you think this is a server error, please contact the webmaster.
    Error 403
    192.168.5.6
    Apache/2.4.37 (Win32) OpenSSL/1.1.1a PHP/7.3.1
```

To fix this, open the file `httpd-xampp.conf` in your XAMPP folder. Find the following line:

```apache
    Require local
```

And change it to:

```apache
    Require all granted
```

### Setting PHPMyAdmin with Credentials

- Open XAMPP Control Panel
<!-- open config.inc.php -->
- Open the file `config.inc.php` in your XAMPP folder or in Xampp Control Panel, click on the `Config` button in the `phpMyAdmin` section.
- Add blowfish secret key. You can generate it using this [https://www.motorsportdiesel.com/tools/blowfish-salt/pma/](https://www.motorsportdiesel.com/tools/blowfish-salt/pma/) or you can use this `blowfish_secret = 'your-secret here'` as your secret key.
- Find the following line:

```php
    $cfg['Servers'][$i]['auth_type'] = 'config';
    $cfg['Servers'][$i]['user'] = 'root';
    $cfg['Servers'][$i]['password'] = '';
    $cfg['Servers'][$i]['extension'] = 'mysqli';
    $cfg['Servers'][$i]['AllowNoPassword'] = false;
```

- Change the `config` to `cookie` and add your credentials.

```php
    $cfg['Servers'][$i]['auth_type'] = 'cookie';
    $cfg['Servers'][$i]['user'] = 'root';
    $cfg['Servers'][$i]['password'] = 'your-password';
    $cfg['Servers'][$i]['extension'] = 'mysqli';
    $cfg['Servers'][$i]['AllowNoPassword'] = false;
```

- Save the file and restart the Apache and MySQL service.

### Grant All Privileges to MySQL User in Any Host

By default the `root` account is not accessible outside your local machine.
It means that you cannot connect to the XAMPP MySQL database over the network, even adding new connection to your database management tool like HeidiSQL and Navicat will not work. but you can use it in your local machine.

To fix this, you need to grant all privileges to your MySQL user in any host.

- Open command prompt and go to your XAMPP folder
- Run the following command:

```console
    mysql -u root -p
```

- Enter your MySQL root password
- Run the following command:

```console
    GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'your_password' WITH GRANT OPTION;
```

- You can replace `root` and `your_password` with your desired MySQL username and MySQL password.
- Run the following command:

```console
    FLUSH PRIVILEGES;
```

- Run the following command:

```console
    exit
```

- Restart the MySQL service in XAMPP

### Configuring Timezone

- Open the file `php.ini` in your XAMPP folder
- Find the following line:

```ini
    ;date.timezone =
```

- Change it to:

```ini
    date.timezone = Asia/Manila ; Change this to your desired timezone
```

- Restart the Apache service in XAMPP

### Changing Apache Ports

By default the Apache port is 80. If you want to change it, you can do it by editing the `httpd.conf` file in your XAMPP folder.

- Open XAMPP control panel
- Click on the `Config` button and select Service and Port Settings tab
- Change the Apache port to your desired port and click on the `OK` button
- Then open the file `httpd.conf` in your XAMPP folder or open XAMPP control panel and click on the `Config` button in Apache section and choose `httpd.conf`
- Find the following line:

```apache
    Listen 80
```

- Change it to:

```apache
    Listen 8080 ; Change this to your desired port
```

- Restart the Apache service in XAMPP

## Configuring FileZilla FTP Server

XAMPP also has FileZilla Server in order for the developer securely tranfer all files via ftp or sftp. By default Filezilla server listen to port 21 and has unlimited user set.

### Changing FileZilla Server Port

- Open XAMPP control panel
- Click on the `Config` button and select Service and Port Settings tab
- Change the FileZilla Server port to your desired port and click on the `OK` button
- Then open the file `FileZilla Server.xml` in your XAMPP folder or open XAMPP control panel and click on the `Config` button in FileZilla Server section and choose `FileZilla Server.xml`
- Find the following line:

```xml
    <Port>21</Port>
```

- Change it to:

```xml
    <Port>2121</Port> ; Change this to your desired port
```

- Restart the FileZilla Server service in XAMPP

### Creating Groups to FileZilla Server

This is optional. You can create groups to your FileZilla Server. By default it has unlimited user set.

**Note:** In these part, the shared directory are the directory where my project located. For example our group project directory name `firstproject` are located under the htdocs folder. Therefore, the directory will be added to this part. If there are more than one project directory for your group, use aliases to display each folder every time you use you FTP account.

- Open XAMPP control panel
- Click on the `Admin` button in FileZilla Server section to open the FileZilla Server interface
- Change the admin password to your desired password
- Then start adding groups and set the shared directory to your project directory

  - Click on the `Groups` icon to open the groups configuration window
  - In the `General` tab, click on the `Add Group` button and add your desired group name
  - Then go to Shared Folders tab and start adding your shared directory

### Creating Groups to FileZilla Server

- Open XAMPP control panel
- Click on the `Admin` button in FileZilla Server section to open the FileZilla Server interface
- Click on the `Users` icon to open the users configuration window
- In the `General` tab, click on the `Add User` button and add your desired username, change the password to your desired password and select the group that you belong, and make sure that the `Enabled` checkbox is checked
- To share project directory, click on the `Shared Folders` tab and add your project directory. If you belong to a group with shared directory, you don't need to add it again.

### Connecting to FileZilla Server

- Open FileZilla Client or any FTP client
- Enter the following details:

```text
    Host: localhost ; Change this to your server ip address or domain name
    Port: 2121 ; Change this to your server port
    Username: your-username
    Password: your-password
```

- Click on the `Quickconnect` button

- If you are using windows explorer, you can also use the following format:

```text
    ftp://username:password@localhost:port
```

- Replace `username`, `password`, `port` with your desired username, password and port.

## Configuring Mercury

Mercury is a web server that is included in XAMPP. It is a lightweight web server that is used for testing and development purposes. By default Mercury listen to port 8080. If you want to change it, you can do it by editing the `mercury.ini` file in your XAMPP folder.

### Changing Mercury Port

- Open XAMPP control panel
- Click on the `Config` button and select Service and Port Settings tab
- Change the Mercury port to your desired port and click on the `OK` button
- Then open the file `mercury.ini` in your XAMPP folder or open XAMPP control panel and click on the `Config` button in Mercury section and choose `mercury.ini`
- Find the following line:

```ini
    Port=8080
```

- Change it to:

```ini
    Port=8081 ; Change this to your desired port
```

- Restart the Mercury service in XAMPP

### Other Configurations

For more information about Mercury, you can watch this video:

[How to setup local email server using XAMPP (Mercury mail)](https://www.youtube.com/watch?v=7dcaUUlsMOg)

## Configuring Tomcat

Tomcat is a web server that is included in XAMPP. It is a lightweight web server that is used for testing and development purposes. By default Tomcat listen to port 8080. If you want to change it, you can do it by editing the `server.xml` file in your XAMPP folder.

### Changing Tomcat Ports

- Open XAMPP control panel
- Click on the `Config` button and select Service and Port Settings tab
- Change the Tomcat port to your desired port and click on the `OK` button
- Then open the file `server.xml` in your XAMPP folder or open XAMPP control panel and click on the `Config` button in Tomcat section and choose `server.xml`
- Find the following line:

```xml
    <Connector port="8080" protocol="HTTP/1.1"
```

- Change it to:

```xml
    <Connector port="8082" protocol="HTTP/1.1" ; Change this to your desired port
```

### Adding Tomcat Role

- Open the file `tomcat-users.xml` in your XAMPP folder or open XAMPP control panel and click on the `Config` button in Tomcat section and choose `tomcat-users.xml`
- Find the following line:

```xml
    <tomcat-users>
```

- Add the following line below:

```xml
    <role rolename="admin-gui"/>
    <role rolename="admin-script"/>
    <role rolename="manager-gui"/>
    <role rolename="manager-script"/>
    <role rolename="manager-jmx"/>
    <role rolename="manager-status"/>
```

- Find the following line:

```xml
    </tomcat-users>
```

- Add the following line above:

```xml
    <user username="admin" password="admin" roles="admin-gui,admin-script,manager-gui,manager-script,manager-jmx,manager-status"/>
```

- Restart the Tomcat service in XAMPP

### Connecting to Tomcat

- Open your browser and enter the following URL:

```text
    http://localhost:8082/manager/html ; Change this to your server ip address or domain name and port
```

- Enter the following details:

```text
    Username: admin
    Password: admin
```

- Click on the `Login` button
