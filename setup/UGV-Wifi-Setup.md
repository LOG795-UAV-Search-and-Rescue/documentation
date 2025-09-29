# UGV Wi-Fi Setup
This document outlines the process for setting up the different Wi-Fi configurations available on the UGV.

## Connection switch via `nmcli` profiles

To make it easier to establish the conection between the UGV and the VOXL drone, we created profiles in `nmcli` to easily switch between the different available configurations.

> [!NOTE]
> It's important to understand that if you are connected through SSH on the UGV, you will get disconnected from the SSH session after switching the connection profile since it changes the UGV's IP address. You will need to reconnect after the operation is done.
>
> If you are connected via wire, you should stay connected throughout the operation.

### 1. Connection to `ETS_5G_Platform`

To connect to the `ETS_5G_Platform` Wi-Fi, simply run the following command in the UGV's terminal.

```shell
sudo nmcli con up 5G-wifi
```

If the IP address is not rotated, it should now be available through `192.168.0.43`.

### 2. Direct connection to the drone (VOXL) Wi-Fi

To connect to the drone's Wi-Fi hotspot directly, you can run the following command in the UGV's terminal.

```shell
sudo nmcli con up drone-wifi
```

The IP of the UGV when on the drone's Wi-Fi is static and should be `192.168.8.2`.

## Adding a new `nmcli` Wi-Fi profile

If you want to add your own Wi-fi profile to the list mentionned earlier, you can run the following command.

```shell
sudo nmcli dev wifi connect "<SSID>" password "<PASSWORD>" name "<PROFILE_NAME>"
```

- `<SSID>` → the Wi-Fi network name (as shown in scans).
- `<PASSWORD> `→ Wi-Fi password (omit password if the network is open).
- `<PROFILE_NAME>` → whatever label you want to manage it (e.g. 5G-wifi, drone-wifi).

Example:
```shell
sudo nmcli dev wifi connect "MyHomeWiFi" password "superSecret123" name cool-new-wifi
```

## Manually connect to another Wi-Fi network (without saving profile)

If you want simply want to connect to another Wi-Fi without saving it as a profile to be re-used in the future, you can run the following command.

```shell
sudo nmcli dev wifi connect "<SSID>" password "<PASSWORD>"
```

- `<SSID>` → the Wi-Fi network name (as shown in scans).
- `<PASSWORD> `→ Wi-Fi password (omit password if the network is open).

This created a temporary conection. If you don't specify `name`, as you would to create a new profile, it auto-generates one.

Example:
```shell
sudo nmcli dev wifi connect "CafeHotspot" password "guest123"
```

## Some other useful `nmcli` commands to view the network

- Show all saved conections:
    ```shell
    sudo nmcli con show
    ```

- Show active conection(s):
    ```shell
    sudo nmcli con show --active
    ```

- Disconnect:
    ```shell
    sudo nmcli con down <PROFILE_NAME>
    ```
