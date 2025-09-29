# VOXL Hotspot Passthrough Setup
This document outlines the process for enabling internet access for clients connected to the **VOXL 2** Wi-Fi hotspot.

> [!warning]
> using the VOXL 2 as a router can cause it to use a lot of its battery if possible all messages to the internet should be minal.*

### 1. Enable Internet Sharing (NAT and DNS)
The modem's connection is private to the VOXL 2. To share it with clients on the Wi-Fi hotspot, you must enable **IP forwarding** and set up **NAT**.

 - **Enable IP Forwarding:** This allows the VOXL 2 to route traffic between its interfaces.
    ``` Bash
    echo 1 > /proc/sys/net/ipv4/ip_forward
    ```

 - **Set Up NAT with ``iptables``:** This rule "masquerades" traffic from the hotspot (``wlan0``) so it appears to originate from the modem (``wwan0``).
    ```Bash
    iptables -t nat -A POSTROUTING -o wwan0 -j MASQUERADE
    ```

 - **Fix DNS Resolution:** It's possible for the clients not to have a DNS while on the hotspot. If the automatic DNS doesn't work then you must manually add one to the client.

### 2. Make Settings Persistent

The changes you made are temporary and will be lost on reboot. The most reliable way to make them permanent is with a ``systemd`` service.

 - **Create a Startup Script:** Create a shell script that contains the commands to enable IP forwarding and set up the iptables rule.
    Create the script file:
    ``` Bash
    nano /usr/local/bin/nat_setup.sh
    ```
    Write in the file:
    ``` Bash
    #!/bin/bash
    echo 1 > /proc/sys/net/ipv4/ip_forward
    iptables -t nat -A POSTROUTING -o wwan0 -j MASQUERADE
    ```
    Make it executable:
    ``` Bash
    chmod +x /usr/local/bin/nat_setup.sh
    ```
 - **Create a systemd Service File:** Create a service file in ``/etc/systemd/system/`` to tell the system to run your script on boot.
    Create the file:
    ``` Bash
    nano /etc/systemd/system/nat_setup.service
    ```
    Write in the file:
    ```
    [Unit]
    Description=NAT Setup for VOXL 2 Cellular Modem
    After=network-online.target
    Wants=network-online.target

    [Service]
    Type=oneshot
    ExecStart=/usr/local/bin/nat_setup.sh
    RemainAfterExit=yes

    [Install]
    WantedBy=multi-user.target
    ```

- **Enable the Service:** Use ``systemctl`` to enable and start the service.
    ``` Bash
    sudo systemctl daemon-reload
    sudo systemctl enable nat_setup.service
    sudo systemctl start nat_setup.service
    ```

You should now share with any devices connected to the VOXL 2 Wi-Fi hotspot the internet comming from the 5G modem.

## See Also
 - [VOXL 5G Setup](VOXL-5G-Setup.md) - Setup a 5G network connection.