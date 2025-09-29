# VOXL 5G Setup
This document outlines the process for setting up a **VOXL 2** with a **Sierra Wireless EM9291 5G modem**.

### 1. Initial Modem Setup 
The VOXL 2 does not use standard Linux networking tools like ``nmcli`` for cellular modems. Instead, it uses a custom utility, ``voxl-modem``. 

- **Access the VOXL 2:** Use ``adb shell`` or ``ssh`` to get a command-line interface on the VOXL.

    Run the following command to connect to via ``adb shell``:
    ``` Bash 
    adb shell 
    ```
   **Note:** To connect via ``adb`` you must be connected with a usb cable to the drone.
   For ``ssh``, the VOXL 2 should already have the hotspot activated out of the box. You need to connect to the hotspot for the ``ssh`` command. In our case the IP address of the VOXL 2 was ``192.168.8.1``. The default user of the VOXL 2 is as follows: 
    ``` JSON
    {
        "user": "root",
        "password": "eolinux123"
    }
    ```

    Run the following command to connect via ``ssh``:
    ``` Bash
    ssh root@192.168.8.1
    ```

 - **Configure the Modem:** Run the ``voxl-configure-modem`` wizard. Select the EM9191 modem option (it works for the EM9291) and enter the APN linked to the SIM card. It's possible you need to enter it manually using the ``custom`` APN since the ``voxl-configure-modem`` wizard was prepared for use in the US.
    ``` Bash 
    voxl-configure-modem
    ```

 - **Reboot the VOXL 2:** This ensures the new modem settings are loaded correctly. 
    ``` Bash 
    reboot 
    ```

    We've found that sometimes the VOXL 2 doesn't reboot properly when rebooting from the shell. It's better to power it OFF and ON again to reboot it.
 

### 2. Verify Modem Connection 

After the reboot, you must verify that the modem has successfully connected to the cellular network and obtained an IP address. 

 - **Check Modem Status:** Run ``systemctl status voxl-modem`` to see if the connection is active. The logs should show a successful connection and IP address lease. The warning ``Too few arguments`` can be ignored. 

    ``` Bash 
    voxl-modem status 
    ```

 - **Confirm Network Interface:** The 5G modem will create a ``wwan0`` network interface. You can verify its IP address using ``ifconfig``. You should see a private IP address (e.g., 100.96.185.228) next to inet. 

    ``` Bash 
    ifconfig wwan0 
    ```
 - **Test Internet Connectivity:** Ping a public IP address to confirm the modem can reach the internet. If this succeeds but pinging a domain name (like google.com) fails, it's a DNS issue. 

    ``` Bash 
    ping -c 4 8.8.8.8 
    ```

 - **Fix DNS Resolution:** If a domain name fails to be pinged, you must manually add a DNS server to the VOXL 2's ``/etc/resolv.conf`` file. (8.8.8.8 is a Google DNS)
    ``` Bash
    echo "nameserver 8.8.8.8" | sudo tee /etc/resolv.conf
    ```

You should now have a fully working 5G internet connection on your VOXL 2.

## See Also
 - [VOXL Hotspot Passthrough Setup](VOXL-Hotspot-Passthrough-Setup.md) - Setup an internet connection for the client of the hotspot.