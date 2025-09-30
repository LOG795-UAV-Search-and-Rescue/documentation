# UGV Firmware Install

## Quick Install
 > [!NOTE]
 > This was taken from the following [documentation](https://github.com/waveshareteam/ugv_jetson) on github.

> [!WARNING]
> After following the documentation we had an issue with the NumPy version. To fix the issue we added the ``numpy==1.26.5`` line in the ``requirements.txt`` provided in the git repo before running the ``setup.sh`` file.

You need to install [Jetson Orin Nano Developer Kit](https://www.waveshare.com/jetson-orin-nano-dev-kit.htm) on your robot if you are using **WAVE ROVER**, **UGV01** or **UGV02**.  

This app is already installed in the **UGV Rover Jetson Orin AI Kit**, **UGV Beast Jetson Orin AI Kit** and **RaspRover Jetson Orin AI Kit**.  

You can use this tutorial to upgrade your robot's upper computer program.  

You can use this tutorial to install this program on a pure Ubuntu(22.04) on Jetson.  


### Download the repo from github

You can clone this repository from Waveshare's GitHub to your local machine.

    git clone https://github.com/waveshareteam/ugv_jetson.git
### Grant execution permission to the installation script
    cd ugv_jetson/
    sudo chmod +x setup.sh
    sudo chmod +x autorun.sh
### Install app (it'll take a while before finish)
    sudo unminimize
    sudo ./setup.sh
### JupyterLab Setup
    python3 create_jupyter_service.py
    sudo mv ugv_jupyter.service /etc/systemd/system/ugv_jupyter.service
    sudo systemctl enable ugv_jupyter
    sudo systemctl start ugv_jupyter
### Volume and Pulseaudio for Multi-user Setup
    pactl set-sink-volume alsa_output.usb-Solid_State_System_Co._Ltd._USB_PnP_Audio_Device_000000000000-00.analog-stereo 100%
    sudo cp pulseaudio.service /etc/systemd/system/pulseaudio.service
    sudo systemctl --system enable --now pulseaudio.service
    sudo systemctl --system status pulseaudio.service
### Service for Jtop
    sudo systemctl enable jtop.service
### Autorun Setup
    ./autorun.sh
### AccessPopup Installation
    cd AccessPopup
    sudo chmod +x installconfig.sh
    sudo ./installconfig.sh
    *Input 1: Install AccessPopup
    *Press any key to exit
    *Input 9: Exit installconfig.sh
### Reboot Device
    sudo reboot

After powering on the robot, Jetson will automatically establish a hotspot, and the OLED screen will display a series of system initialization messages:  

![](./media/RaspRover-LED-screen.png)
- The first line `E` displays the IP address of the Ethernet port, which allows remote access to the Raspberry Pi. If it shows No Ethernet, it indicates that the Raspberry Pi is not connected to an Ethernet cable.
- The second line `W` indicates the robot's wireless mode. In Access Point (AP) mode, the robot automatically sets up a hotspot with the default IP address `192.168.50.5`. In Station (STA) mode, the Raspberry Pi connects to a known WiFi network and displays the IP address for remote access.
- The third line `F/J` specifies the Ethernet port numbers. Port `5000` provides access to the robot control Web UI, while port `8888` grants access to the JupyterLab interface.
- The fourth line `STA` indicates that the WiFi is in Station (STA) mode. The time value represents the duration of robot usage. The dBm value indicates the signal strength RSSI in STA mode.  


You can access the robot web app using a mobile phone or PC. Simply open your browser and enter `[IP]:5000` (for example, `192.168.10.50:5000`) in the URL bar to control the robot.  

To access JupyterLab, use `[IP]:8888` (for example, `192.168.10.50:8888`).  

If the robot is not connected to a known WiFi network, it will automatically set up a hotspot named "`AccessPopup`" with the password `1234567890`. You can then use a mobile phone or PC to connect to this hotspot. Once connected, open your browser and enter `192.168.50.5:5000` in the URL bar to control the robot.  

To ensure compatibility with various types of robots running on Raspberry Pi, we utilize a config.yaml file to specify the particular robot being used. You can configure the robot by entering the following command:

    s 22

In this command, the s directive denotes a robot-type setting. The first digit, `2`, signifies that the robot is a `UGV Rover`, with `1` representing `RaspRover` and `3` indicating `UGV Beast`. The second digit, also `2`, specifies the module as `Camera PT`, where `0` denotes `Nothing` and `1` signifies `RoArm-M2`.  
