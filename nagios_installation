1. Connect to your AWS Linux instance via SSH.

2. Update your system packages:
```bash
sudo yum update -y
```

3. Install required dependencies:
```bash
sudo yum install -y gcc glibc glibc-common make gettext automake autoconf wget openssl-devel net-snmp net-snmp-utils httpd php perl gd gd-devel
```

4. Create a Nagios user and group:
```bash
sudo useradd nagios
sudo groupadd nagcmd
sudo usermod -a -G nagcmd nagios
sudo usermod -a -G nagcmd apache
```

5. Download and install Nagios Core:
```bash
cd /tmp
wget https://github.com/NagiosEnterprises/nagioscore/archive/nagios-4.5.9.tar.gz
tar -zxvf nagios-4.5.9.tar.gz
cd nagioscore-nagios-4.5.9/
```

6. Configure and compile Nagios:
```bash
./configure --with-httpd-conf=/etc/httpd/conf.d
make all
sudo make install
sudo make install-init
sudo make install-daemoninit
sudo make install-commandmode
sudo make install-config
sudo make install-webconf
```

7. Create a password for the Nagios web interface:
```bash
sudo htpasswd -c /usr/local/nagios/etc/htpasswd.users nagiosadmin
```

8. Download and install Nagios Plugins:
```bash
cd /tmp
wget https://github.com/nagios-plugins/nagios-plugins/releases/download/release-2.4.11/nagios-plugins-2.4.11.tar.gz
tar -zxvf nagios-plugins-2.4.11.tar.gz
cd nagios-plugins-2.4.11/
./configure --with-nagios-user=nagios --with-nagios-group=nagios
make
sudo make install
```

9. Start and enable Apache and Nagios services:
```bash
sudo systemctl start httpd
sudo systemctl enable httpd
sudo systemctl start nagios
sudo systemctl enable nagios
```

10. Configure your AWS security group to allow inbound HTTP traffic (port 80) to access the Nagios web interface.

11. Access the Nagios web interface by navigating to http://your-instance-public-ip/nagios in your browser and logging in with the "nagiosadmin" username and the password you created.
