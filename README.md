# OpenVPN autostart Linux

Modify OpenVPN Configuration
-------------
Open a terminal and run the following command to edit the configuration file:



    sudo nano /etc/default/openvpn

Inside the file, locate the line:



    #AUTOSTART="all"

Remove the `#` and save the changes.

Execute the following commands to display the available .ovpn configuration files:

    cd /etc/openvpn
    ls

Choose the .ovpn file you want to use for automatic connection. Rename it to client.conf, as this is the standard naming convention in OpenVPN. Use the following command:

    sudo cp vpnserver.ovpn client.conf

Replace `"vpn.ovpn"` with the actual filename of your VPN configuration file.

Access the file `client.conf`:

    sudo nano client.conf

Modify the following line:
    	
    auth-users-pass
to

    auth-users-pass .secrets
	
Save the changes and exit.

Modify the file `.secrets`

    sudo nano .secrets

Enter your username on the first line and your password on the second, then save.

    username
    password

Enable the systemd service
-------------
Run the following command to enable OpenVPN to start at boot:

    sudo systemctl enable openvpn@client.service
Then, reload the systemd daemons:

    sudo systemctl daemon-reload

Now, start OpenVPN using this command:

    sudo service openvpn start

Test the Configuration
-------------
Reboot the system with the command:

    reboot

To verify your external IP, run the following command:

    curl ipinfo.io
