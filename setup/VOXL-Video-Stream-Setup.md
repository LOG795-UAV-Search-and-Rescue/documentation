# VOXL Video Stream Setup

This document outlines the different things that were done in order to have an **RTSP** stream that be read with WebRTC on any device on the same network as the drone (VOXL).

## Overview

The system has three main components:

| Component         | Role                                                           | Notes                                    |
| ----------------- | -------------------------------------------------------------- | ------------------------------------------ |
| **voxl-streamer** | Streams camera feed as **RTSP** (`rtsp://127.0.0.1:8900/live`) | Comes preinstalled with the base VOXL image                  |
| **MediaMTX**      | Converts **RTSP** -> **WebRTC** (WHEP) for broswer playback    | Application that needs to be installed on the VOXL                   |
| **Go UI**         | Serves the embedded web UI                                     | Application built for this project specifically. It must be built on the VOXL and launched manually |

The final result:
- A live, low-latency (< 500ms) video directly in a web broswer.
- A local web interface accessible at: http://192.168.8.1:8080
    > [!IMPORTANT]
    > To access http://192.168.8.1:8080, make sure that you are on the `VOXL-476723235` Wi-Fi (password for that Wi-Fi is : `1234567890`).
- Automatically tries to reconnect to the video stream from the user interface when a deconnection occurs.

## 1. VOXL Base Services

Ensure that the following services are configured as shown:
- voxl-streamer
- voxl-camera-server
- ...

Check if you have those services `enabled` and `running`.
```shell
voxl-inspect-services
```

If one of the services listed above is not `enabled`, not `running` or both, follow these steps:

1. If `voxl-streamer` is not running :
   1. Enable it :
        ```shell
        sudo systemctl enable voxl-streamer
        sudo systemctl start voxl-streamer
        ```
    2. Configure it :
        ```shell
        sudo nano /etc/modalai/voxl-streamer.conf
        ```
        and replace the contents of that file for this :
        ```json
        {
            "input-pipe": "hires_down_small_encoded",
            "rotation": 0,
            "decimator": 1,
            "encoder": "h264",
            "port": 8900,
            "bitrate": 1000000
        }
        ```
    3. Restart it to apply the new configuration :
        ```shell
        sudo systemctl enable voxl-streamer
        sudo systemctl start voxl-streamer
        ```

2. If the `voxl-camera-server` is not running :
   1. Enable it :
        ```shell
        sudo systemctl enable voxl-camera-server
        sudo systemctl start voxl-camera-server
        ```
    2. Configure it :
        ```shell
        voxl-configure-cameras
        ```
        and select this option: `28 - M0173 Starling 2 Max dual IMX412  + dual AR0144`. (It might not be the configuration with ID `28` but the description should match if you are using a Starling 2 Max drone).
    3. Restart it to apply the new configuration
        ```shell
        sudo systemctl enable voxl-camera-server
        sudo systemctl start voxl-camera-server
        ```

3. Confirm that the video stream works:\
    We recommend testing with **VLC** as it supports **RTSP** natively.
    > [!IMPORTANT]
    > To access http://192.168.8.1:8900/live, make sure that you are on the `VOXL-476723235` Wi-Fi (password for that Wi-Fi is : `1234567890`).
    ```shell
    vlc rtsp://192.168.8.1:8900/live
    ```
    > [!TIP]
    > If it does not work, it is most likely due to a bad configuration. We recommand reconfiguring the camera and streamer services to make sure that everything works well together.

## 2. MediaMTX (If not already installed and configured)

MediaMTX is a lightweight **RTSP**/**WebRTC** server that repackages **RTSP** from VOXL into a **WHEP** (WebRTC-HTTP Egress Protocol) stream compatible with browsers.

### Download & Install

Since the VOXL drone isn't connected to the internet, we recommend downloading the `tar.gz` file on your personnal computer and upload it to the drone with **SCP**.

1. Download it here: https://github.com/bluenviron/mediamtx/releases/download/v1.15.3/mediamtx_v1.15.3_linux_arm64.tar.gz.\
    Don't hesitate to use a later version than displayed here, it shouldn't break anything.

2. Upload it to the drone and unzip it with:
    ```shell
    tar -xzf mediamtx_*.tar.gz
    ```

3. You can then move the folder anywhere you'd like. Keep it in a place that you won't accidently delete.

4. Then, it needs to be configured by accessing the `mediamtx.yml` file that is inside the mediamtx folder that you just moved to a secure location. You can paste this configuration at the end of the file where you see the `paths:` key in the configuration `yml` file:
    ```shell
    paths:
      drone:
       source: rtsp://127.0.0.1:8900/live
    ```

5. We finally want it to auto-start by adding a service for **MediaMTX** :
    > [!IMPORTANT]
    > Make sure to change `<path-to-mediamtx>` in the command below for the path to your mediamtx folder. Example: `/home/voxl/mediamtx`.
    ```shell
    sudo tee /etc/systemd/system/mediamtx.service > /dev/null <<'EOF'
    [Unit]
    Description=MediaMTX Stream Gateway
    After=network.target

    [Service]
    WorkingDirectory=/<path-to-mediamtx>
    ExecStart=/<path-to-mediamtx>/mediamtx
    Restart=always
    User=voxl

    [Install]
    WantedBy=multi-user.target
    EOF

    sudo systemctl daemon-reload
    sudo systemctl enable mediamtx
    sudo systemctl start mediamtx
    ```
    Check if it started correctly :
    ```shell
    systemctl status mediamtx
    ```

## 3. Go User Interface Application

The Go app handles:
    - Services an embedded HTML/JS interface on port `8080`.
    - Proxies WebRTC (WHEP) requests to MediaMTX (`127.0.0.1:8889`).

### Project structure
```shell
drone-code/
├── README.md
└── client/
    ├── go.mod
    ├── main.go           # main project
    ├── send_to_drone.sh  # 
    └── static/           # web interface
        ├── app.js
        ├── index.html
        └── style.css
```

### Build and run

> [!IMPORTANT]
> To access http://192.168.8.1:8080/, make sure that you are on the `VOXL-476723235` Wi-Fi (password for that Wi-Fi is : `1234567890`).

From project root:

```bash
cd client
go build
./drone-code
```

Open in broswer:
```shell
http://192.168.8.1:8080/
```

You should see:
- A live video feed.
- A "Call UGV robot" button.
- Logs in the terminal when pressed.

## 4. Typical Run Sequence

> [!IMPORTANT]
> Wi-fi is `VOXL-476723235` with password : `1234567890`.

1. Boot VOXL and conect to its Wi-Fi (should be `192.168.8.1`).
2. `voxl-streamer` auto-starts and provides RTSP feed.
3. `mediamtx` starts and repackages the feed.
4. `drone-code` binary runs automatically or manually:
    ```shell
    ./drone-code
    ```
5. Access `http://192.168.8.1:8080/`

## TroubleShooting
| Problem | Likely Cause | Fix |
| - | - | - |
| 404 on `/whep/drone` | Wrong proxy route | Ensure Go uses `mux.Handle("/whep/", proxy)` **without stripPrefix** |
| no stream is available on path "whep/drone" | Path mismatch | JS must use `/drone/whep` **OR** `/whep/drone`, maching MediaMTX |
| `/drone` works but `/whep` fails | RTSP path typo | Check `mediamtx.yml` uses correct `source` |
| Stuttering / latency | VOXL overloaded | Disable unused services (`voxl-tag-detector`, `voxl-flow-server`, etc.) |
| No video | Stream path invalid | Test `rtsp://127.0.0.1:8900/live` in VLC |
| Proxy 404 | UI running off-drone | Update GO constant: `mediaMTXOrigin = "http://192.168.8.1:8889"` |

## Maintenance

**Update MediaMTX**
```shell
cd /PFE/mediamtx
killall mediamtx
curl -L -o mediamtx.tar.gz https://github.com/bluenviron/mediamtx/releases/latest/download/mediamtx_linux_arm64.tar.gz
tar -xzf mediamtx.tar.gz --overwrite
./mediamtx --version
```

**Restart the whole stack**
```shell
cd /PFE/code
sudo systemctl restart voxl-streamer
sudo systemctl restart mediamtx
sudo ./drone-code
```
