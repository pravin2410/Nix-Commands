# Nix-Commands
Basic Nix command

1. a)Check the load on your server using the uptime command
b)cat /proc/meminfo will show you free available memory in server

2.Create a new file called nginxReloader.sh that will use inotify-tools to listen for filesystem events and then automatically reload Nginx.

we will use nginx -s reload command for auto updating file in /etc/nginx/sites-enabled/ directory

3.a)we need to enable NGINX access and error log. To do that we have go to below path
To do that, edit the Nginx configuration file and add the following access_log directive.
server {
...
...
        access_log /var/log/nginx/access_log combined;
...
...
}

Error.log :

server {
...
...
         error_log /var/log/nginx/error_log debug;
...
...
}

Once done with enabling access log and log level of error log to debug, restart Nginx and tail the log file to see them in real time.

# systemctl restart nginx
# tail -f /var/log/nginx/access_log
# tail -f /var/log/nginx/error_log


4.we need to use sudo fuser -k 8000/tcp. This should kill all the processes associated with port 8000.


5.a)number of occurrences of that typo in the source code file without opening the file
grep -o -i typo sourcecode.txt | wc -l



b)occurence of that typo with respect to line number of file

 grep -n 'typo' sourcecode.txt

7.To check a service's status, use the systemctl status service-name command.
$ sudo systemctl status sshd

To cgecj the log we have to use below command
journalctl -u service-name.service

it will shoy you logs of that service

9.we have to follow below steps :

Step 1: Head over to EC2 –> Volumes and create a new volume of your preferred size and type.

Step 2: Select the created volume, right-click and select the “attach volume” option.

Step 3: Select the ec2 instance from the instance text box

Step 4: Now, login to your ec2 instance and list the available disks using the following command. lsblk

The above command will list the disk you attached to your instance.

Step 5: Check if the volume has any data using the following command.

sudo file -s /dev/xvdf
If the above command output shows “/dev/xvdf: data“, it means your volume is empty.

Step 6: Format the volume to the ext4 filesystem using the following command.

sudo mkfs -t ext4 /dev/xvdf
Alternatively, you can also use the xfs format. You have to use either ext4 or xfs.

 sudo mkfs -t xfs /dev/xvdf
Step 7: Create a directory of your choice to mount our new ext4 volume. I am using the name “newvolume“. 

sudo mkdir /newvolume
Step 8: Mount the volume to “newvolume” directory using the following command.

sudo mount /dev/xvdf /newvolume/
Step 9: cd into newvolume directory and check the disk space to validate the volume mount.

cd /newvolume
df -h .
The above command should show the free space in the newvolume directory.

To unmount the volume, use the unmount command as shown below..

umount /dev/xvdf

10. we have to follow below steps to install Http server on linux.

a)install http server
$ yum install httpd

b)Create the directory where you will copy the full Oracle Linux Release 6 Media Pack DVD image, for example /var/www/html/OSimage/OL6.6:
$ mkdir -p /var/www/html/OSimage/OL6.6

c)Edit the HTTP server configuration file, /etc/httpd/conf/httpd.conf, as follows:

i)Specify the resolvable domain name of the server in the argument to ServerName.
ServerName server_addr:80

ii)If the server does not have a resolvable domain name, enter its IP address instead. For example, the following entry would be appropriate for an HTTP server with the IP address 192.168.1.100.
ServerName 192.168.1.100:80

iii)If the directory to which you will copy the DVD image in not under /var/www/html, change the default setting of DocumentRoot.
DocumentRoot "/var/www/html"

iv)Verify that the <Directory> setting points to the same setting as DocumentRoot.
<Directory "/var/www/html">

v)If you want to be able to browse the directory hierarchy, verify that the Options directive specifies the Indexes option, for example:

Options Indexes FollowSymLinks

vi)Save your changes to the file.

d)Start the Apache HTTP server, and configure it to start after a reboot.

$ service httpd start
$ chkconfig httpd on

e)If you have enabled a firewall on your system, configure it to allow incoming HTTP connection requests on TCP port 80.

For example, the following command configures iptables to allow incoming HTTP connection requests and saves the change to the firewall configuration:

iptables -I INPUT -p tcp -m state --state NEW -m tcp --dport 80 -j ACCEPT
service iptables save

Once http is installed on linux then we can install MySQl.

We need to perform below steps :

i)we first want to make sure our linux server is up to date.
sudo apt-get update
sudo apt-get upgrade
this will perform necessary update and upgrade

ii)sudo apt-get install mysql-server
This command will install the latest version of MySQL

iii)we can check whether MySQl is working right or not by entering below command
mysql -u username -p

it will be promoted to enter in the password. These are the steps which used for installation.
