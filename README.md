Aim:Install DHCP Server in Ubuntu 16.04
sudo apt-get update
sudo apt-get install isc-dhcp-server
sudo nano /etc/default/isc-dhcp-server  (● Assign the network interface: "ens33"
sudo nano /etc/dhcp/dhcp.conf (comment option domain name and uncomment authorative)
cd /etc/dhcp/
ls
sudo systemctl start isc-dhcp-server
sudo systemctl status isc-dhcp-server
sudo systemctl enable isc-dhcp-server
sudo su
sudo ufw status
dhcp-lease-list
ls
dhcp
exit
*client
sudo su
sudo nano/etc/network/interfaces  (if iface inet ens33 show no changes)
ip a

*server
sudo nano /var/lib/dhcp/dhcpd.lease


practical 3
Aim configure NTP server (NPTd), install and configure NTPd, config NTP client (ubuntu & windows)
sudo apt-get update 
sudo apt-get install ntp
sudo nano /etc/ntp.conf
server 0.europe.pool.ntp.org
server 1.europe.pool.ntp.org
server 2.europe.pool.ntp.org
server 3.europe.pool.ntp.org
sudo systemctl restart ntp
sudo systemctl status ntp
sudo ufw allow ntp
sudo ufw allow 123/ntp
sudo ufw allow reload
client
sudo apt-get update
sudo apt-get install ntpdate
sudo /etc/hosts    10.128.021[server ip address]  cs[hostname]
sudo ntpdate NTP-server-hostname (sudo ntpdate cs)
sudo timedatectl set-ntp off
sudo apt-get install ntp
sudo nano /etc/ntp.conf
server boinic prefer iburst
sudo systemctl restart ntp
ntpq -p


practical 4
Aim: SSH server  Password Authentication
configure SSH server to manage a server from the remote computer, SHH Client:(ubuntu and windows)
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install openssh-server
sudo nano /etc/ssh/ssh_config
uncomment port22 and add a lineMaxAuthTries4
sudo service ssh status
sudo service ssh start
ifconfig
on cmd:ping ip address
open putty login run ls command
cd Downloads
/Downloads$ ls
/Downloads$ touch testfiledemo
/Downloads$ ls
/Downloads$ cd
ls

on ubuntu run command 
ssh cs@192.168.173.128 -p22
ls
touchdemo
ls


practical 6
Aim: configure DHCP server configure DHCP(dynamic host configuration protocol)....
server 
sudo apt-get install isc-dhcp-server
ifconfig
sudo nano /etc/default/isc-dhcp-server (INTERFACES="ens33")
cd /etc/dhcp
ls
sudo nano /etc/dhcp/dhcpd.conf
(comment the option domain-name "example.org";
option domainname-server ns1.example.org, ns2.example.org;)
(uncommentauthorative)
and update A slightly subnet
sudo systemctl start isc-dhcp-server
sudo systemctl status isc-dhcp-server
sudo systemctl enable isc-dhcp-server
sudo ufw status 
dhcp-lease-list
client
sudo nano /etc/network interfaces
(should show auto ens33 and iface inet dhcp lines)
server side 
dhcp sudo nano /var/lib/dhcp/dhcpd.leases
client
sudo systemctl restart networking
ip a
server 
sudo apt-get update 
sudo apt-get install nfs-kernel-server
sudo mkdir /public
sudo mkdir /private
sudo chmod 755 /public/
sudo chmod 777 /private
sudo nano /etc/exports
(Add lines at end /public *(ro,sync,no_subtree_check)
/private 192.168.173.100(rw,sync,no_subtree_check)
sudo exportfs -arvf
restart nfs-kernel-server and enable and status
client
sudo apt-get update
sudo apt-get install nfs-common
showmount -e 192.168.173.132
sudo mkdir /mnt/public
sudo mkdir /mnt/private
sudo mount -t nfs 192168.173.132:/public/mnt/public
sudo mount -t nfs 192.168.173.132:/private/mnt/private
mount
if uncorrect mount done then use umount and unmont /mnt/public
sudo nano /etc/fstab
(Add lines 192.168.173.132:/public /mnt/public nfs defaults,_netdev 0 0
 192.168.173.132:/private /mnt/private nfs defaults,_netdev 0 0
mount -a
cd /mnt/public
ls
touch file
ll


practical 7
Aim:configure ldap 
sudo apt-get install slapd ldap-utils(
systemctl status slapd
sudo dpkg-reconfigure slapd
ldapwhoami -H ldap:// -x
sudo nano /etc/ldap/ldap.conf
add URI ldap://localhost
idapsearch -x
sudo apt install phpldapadmin
sudo nano /etc/phpldapadmin/config.php
set time zzone $ config>custom>appearance['timezone'] = 'Asian/kolkata';
set:-server.setvalue('server','name' ,'Example LDAP Server');
ip a
server.setvalue('server', 'host', '192.168.173.132')
uncomment and chage false in true (config.custom.appearence['hide_template_warning] = true;
server.setvalue('login','anon_bind',false change true in false ) array line uncomment
server>setvalues('login',bind_id,'cn=admin,dc=example,dc=com');
search on your ip addess and /phpldapadmin



practical 9
Aim:install mysql to configure dtabase server,install phpmyadmin to operate mysql on web browser from client
sudo apt-get install apache2
inside varwwwhtml 
indexhtml click
sudo service apache2 stop
sudo service apache2 start
sudo chmod -R 777 /var/www/html
create text.html
write inside ekta
sudo apt-get install php
sudo service apache2 restart
create test.php foldr
write inside <php
phpinfo();
?>
sudo apt install libapache2-mod-php
search for localhost/test.php
sudo apt-get install mysql-server mysql-client
root passwd 123456
mysql -u root -p
show databases;
exit
sudo apt-get install phpmyadmin
configure database for phpmyadmin with dhconfig-common : CLICK NO
sudo service apache restart
search localhost/phpmyadmin



practical 10
Aim:install samba to share folders or files btw windows and linux
sudo apt update -y
sudo apt install samba -y
sudo mkdir /share
sudo chmod 777 /share
sudo nano /etc/samba/smb.conf
write:-[my-samba-share]
            path = /share 
            public = no
            valid users = tom, harry 
            read list = tom
            write list = jerry 
            browseable = yes
            comment = "My Samba File Server"
sudo testparm
sudo adduser tom -s /bin/nologin
sudo adduser jerry -s /sbin/nologin
sudo smbpasswd -a tom
sudo smbpasswd -a jerry
sudo systemctl start smbd
sudo systemctl start nmbd
sudo systemctl enable smbd nmbd
ip a
ping ip address
go to connect to server and type smb://ipaddress
then open mysamba share
create tom registration
open cmd: ping ipaddress
window + R
and type \\ipaddress
login for jerry



















































































































































































































































































































































































































































































































































































































































































