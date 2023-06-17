
You may also wish to have graphical user interface (GUI) desktop for your server instead of a command-line only ssh terminal interface. To do this, you must install a VNCserver

# install VNC server

Download setup to the storage bucket we created

Download the setup files here: https://github.com/developerpiru/cloudservers/blob/master/VNC-setup.tar.gz

open SSH 

you can see downloaded vnc server file in mount folder

```
cd mountfolder/path/to/where/you/saved/the/file

tar -xzvf VNC-setup.tar.gz

cd VNC-setup

bash vnc-setup.sh

```

# install realvnc viwer in windows machine 

by creating account in realvnc we download and signin to realvnc 


# setup firewall in VM machine , so we can allow port or external IP 


Firewall normally wont allow vnc 
so it is necessary to create firewall rule to allow TCP 5901

search firewall rule in cloud account .
create firewall rule and fill details . more important are Name (vnc-server) , tags (vnc-server) and TCP : 5901
server IP4  =  0.0.0.0/0


and allow 
save firewall

Go to VM machine instance

fill network tags = vnc-server



# On your VM, start the VNC server with this command:

vncserver -geometry 1200x1050
Note: the -geometry 1200x1050 flag is optional and you can customize it to any resolution you prefer

Open your VNC client (PuTTY or VNC Viewer) and enter the external IP address (not its local IP!) of your remote computer followed by the :5901 port. For example: 192.0.2.0:5901. You can find the external IP address of your VM by looking at your VM instances list.


```
sudo apt-get update

sudo apt-get install tightvncserver

sudo reboot 

```

# check whether external IP working by typing

nc externalIPAddress 5901

```
nc 192.0.2.0:5901 

```

It has to show 
RFS 3:00 time 