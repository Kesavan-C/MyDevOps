---

## How to Install Nagios Core on AWS Linux Instance

Follow the steps below to install and configure Nagios Core on your AWS Linux instance.

### 1. Connect to Your AWS Linux Instance via SSH

SSH into your AWS instance using your preferred terminal.

### 2. Update System Packages

Run the following command to ensure your system is up-to-date:

```bash
sudo yum update -y
```

### 3. Install Required Dependencies

Install the necessary dependencies using the command below:

```bash
sudo yum install -y gcc glibc glibc-common make gettext automake autoconf wget openssl-devel net-snmp net-snmp-utils httpd php perl gd gd-devel
```

### 4. Create Nagios User and Group

Create the required user and group for Nagios and add the Apache user to the `nagcmd` group:

```bash
sudo useradd nagios
sudo groupadd nagcmd
sudo usermod -a -G nagcmd nagios
sudo usermod -a -G nagcmd apache
```

### 5. Download and Install Nagios Core

Download and extract the Nagios Core source code:

```bash
cd /tmp
wget https://github.com/NagiosEnterprises/nagioscore/archive/nagios-4.5.9.tar.gz
tar -zxvf nagios-4.5.9.tar.gz
cd nagioscore-nagios-4.5.9/
```

### 6. Configure and Compile Nagios

Run the following commands to configure, compile, and install Nagios Core:

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

### 7. Set Up a Password for the Nagios Web Interface

Create a user for accessing the Nagios web interface by setting a password:

```bash
sudo htpasswd -c /usr/local/nagios/etc/htpasswd.users nagiosadmin
```

### 8. Download and Install Nagios Plugins

Download and install the necessary Nagios plugins:

```bash
cd /tmp
wget https://github.com/nagios-plugins/nagios-plugins/releases/download/release-2.4.11/nagios-plugins-2.4.11.tar.gz
tar -zxvf nagios-plugins-2.4.11.tar.gz
cd nagios-plugins-2.4.11/
./configure --with-nagios-user=nagios --with-nagios-group=nagios
make
sudo make install
```

### 9. Start and Enable Apache and Nagios Services

Start the Apache and Nagios services and enable them to start on boot:

```bash
sudo systemctl start httpd
sudo systemctl enable httpd
sudo systemctl start nagios
sudo systemctl enable nagios
```

### 10. Configure AWS Security Group for HTTP Access

Make sure your AWS security group allows inbound HTTP traffic (port 80) so you can access the Nagios web interface.

### 11. Access the Nagios Web Interface

Finally, navigate to the following URL in your browser to access the Nagios web interface:

```
http://<your-instance-public-ip>/nagios
```

Log in with the `nagiosadmin` username and the password you created earlier.

---
