<style>
    th {
        text-align: left;
        background-color: #f0f0f0ff;
        text-wrap: nowrap;
    }

    .note {
        color: black; 
        border: 1px solid #3391FE; 
        background-color: #B9DAFF; 
        padding: 10px; 
        border-radius: 5px;
        margin-bottom: 1em
    }
</style>

# Incident Report
## Report Summary

<table>
  <tr>
    <th>Owner</th>
    <td>Raphaël Camara</td>
  </tr>
  <tr>
    <th>Incident</th>
    <td>The ModalAI VOXL Starling 2 Max crashed causing it to break most structural pieces and stopping the developpement of our project.</td>
  </tr>
  <tr>
    <th>Date of fact</th>
    <td>2025-12-03 at 13h07</td>
  </tr>
</table>

<div style="color: black; border: 1px solid #3391FE; background-color: #B9DAFF; padding: 10px; border-radius: 5px; margin-bottom: 1em">
ℹ️ <strong>Incident summary:</strong> On the 3rd of december 2025, at approximatly 13h07, during a flight demonstration of our application, we lost communication to the drone indoors causing it to gain altitude uncontrollably. With no way to stop it, the drone hit the ceiling after which it came crashing down from about 30 feet in the air. Because of that, we lost the propellers, the feet, the 5G antenna and the battery clips due to breakage. Luckily, none of the computational chips were damaged severely. 
</div>

| Instruction | Report |
| ----------- | ------ |
| **Leadup**      | We started preping for a test flight at around 10h30, figuring how the drone would fly and adding some black tape to the ground to help the drone stabilies using the camera captors. At around 12h00, we setup the drone to fly with indoors flight configurations. With a bit of confidence from the test flights, we started to prepare for a demonstration of our application, which is to give directive to a rover using the drone as a source. To ensure the functionnality we tested with the drone in our hands, the rover was properly following the drone. We set out to make a full demonstration at around 13h06, at first the drone was flying fine but it started deviating from our controler inputs at which point the incident happend. |
| **Fault**       | The drone moved on its own and didn't respond to controller input. |
| **Timeline**    | 10h30: Prep phase<br/>12h00: Test flights (no issues)<br/>13h06: Start of demonstration, rover follows drone from the ground.<br/>13h07: Drone crashes|
| **Root cause**  | After revewing the logs that we got from the QGroundControl WebApp we found a single RTL activation which was at the start of the incident. We strongly believe that the automatic activation of the RTL caused the unexpected behavior of the drone. |
| **Damage**      | Shattered propellers, exploded feet, antenna ripped out of the feet, battery clip split in pieces |


## Annex
### Logs in QGroundControl
```
[13:07:01.373 ] Critical: Kill-switch engaged
[13:07:01.373 ] Info: Disarmed by RC (switch)
[13:07:01.373 ] Critical: Switching to mode 'RTL' is currently not possible
- RTL switch engaged
- No valid global position estimate

[13:07:01.373 ] Info: Pilot took over using sticks
[13:07:01.373 ] Critical: Switching to mode 'Hold' is currently not possible
- RTL switch engaged
- No valid global position estimate

[13:07:01.373 ] Info: Pilot took over using sticks
[13:07:01.373 ] Info: Takeoff detected
[13:07:01.373 ] Info: Armed by RC (switch)
[13:07:01.117 ] Info: RTL activated
[13:07:01.117 ] Info: Using minimum takeoff altitude: 2.50 m
[13:07:01.117 ] Info: Using minimum takeoff altitude: 2.50 m
[13:07:01.117 ] Info: logging: opening log file 2025-11-17/20_17_18.ulg
[13:07:01.021 ] Info: Disarmed by RC (switch)
[13:07:00.842 ] Critical: Switching to mode 'RTL' is currently not possible
No valid global position estimate
[13:07:00.842 ] Info: Pilot took over using sticks
[13:07:00.842 ] Critical: Switching to mode 'Hold' is currently not possible
No valid global position estimate
[13:07:00.842 ] Info: Pilot took over using sticks
[13:07:00.842 ] Info: Takeoff detected
[13:07:00.842 ] Info: Armed by RC (switch)
[13:07:00.841 ] Info: Using minimum takeoff altitude: 2.50 m
[13:07:00.841 ] Info: Using minimum takeoff altitude: 2.50 m
[13:07:00.841 ] Info: logging: opening log file 2025-11-17/20_17_18.ulg
[13:06:19.971 ] Critical: Switching to mode 'Hold' is currently not possible
No valid global position estimate
[13:06:15.846 ] Info: Pilot took over using sticks
[13:06:12.415 ] Info: Takeoff detected
[13:06:12.415 ] Info: Armed by RC (switch)
[13:06:08.455 ] Info: Armed by RC (switch)
[12:51:55.223 ] Info: Disarmed by landing
[12:51:55.223 ] Info: Landing detected
[12:49:31.353 ] Critical: Switching to mode 'Hold' is currently not possible
No valid global position estimate
[12:49:25.437 ] Info: Takeoff detected
[12:49:19.130 ] Info: Pilot took over using sticks
[12:49:19.130 ] Info: Armed by RC (switch)
[12:49:14.412 ] Info: Armed by RC (switch)
[12:33:00.868 ] Info: Disarmed by landing
[12:33:00.848 ] Info: Landing detected
[12:31:25.203 ] Critical: Switching to mode 'Hold' is currently not possible
No valid global position estimate
[12:31:23.849 ] Info: Pilot took over using sticks
[12:31:19.464 ] Info: Takeoff detected
[12:31:19.464 ] Info: Armed by RC (switch)
[12:31:19.464 ] Info: Disarmed by landing
[12:31:19.464 ] Info: Landing detected
[12:31:19.464 ] Info: Pilot took over using sticks
[12:31:19.464 ] Info: Takeoff detected
[12:31:19.315 ] Info: Using minimum takeoff altitude: 2.50 m
[12:31:14.953 ] Info: logging: opening log file 2025-11-17/20_11_8.ulg
[12:31:14.953 ] Info: Using minimum takeoff altitude: 2.50 m
[12:31:14.953 ] Info: logging: opening log file 2025-11-17/20_10_56.ulg
[12:31:14.953 ] Info: Armed by RC (switch)
[12:31:08.891 ] Info: Disarmed by landing
[12:31:08.782 ] Info: Landing detected
[12:31:07.928 ] Info: Pilot took over using sticks
[12:31:07.070 ] Info: Takeoff detected
[12:31:06.922 ] Info: Armed by RC (switch)
[12:31:04.165 ] Info: Armed by RC (switch)
[12:31:02.982 ] Info: Armed by RC (switch)
[12:27:55.177 ] Critical: Manual control lost
[12:25:53.035 ] Critical: Arming denied: switch to manual mode first
[12:25:49.356 ] Info: Kill-switch engaged
[12:22:04.443 ] Info: Disarmed by landing
[12:22:04.334 ] Info: Landing detected
[12:21:16.392 ] Critical: Failsafe activated, triggering fallback to altitude control
No valid local position estimate
[12:20:37.963 ] Critical: Switching to mode 'Hold' is currently not possible
No valid global position estimate
[12:20:35.793 ] Info: Pilot took over using sticks
[12:20:31.956 ] Info: Takeoff detected
[12:20:31.955 ] Info: Armed by RC (switch)
[12:20:28.277 ] Info: Armed by RC (switch)
[12:19:15.352 ] Critical: Manual control lost
[12:16:13.320 ] Info: Disarmed by landing
[12:16:13.277 ] Info: Landing detected
[12:15:25.409 ] Critical: Switching to mode 'Hold' is currently not possible
No valid global position estimate
[12:15:24.172 ] Critical: Switching to mode 'Hold' is currently not possible
No valid global position estimate
[12:15:22.774 ] Info: Pilot took over using sticks
[12:15:22.629 ] Critical: Switching to mode 'Hold' is currently not possible
No valid global position estimate
[12:15:21.573 ] Critical: Switching to mode 'RTL' is currently not possible
No valid global position estimate
[12:15:20.520 ] Critical: Switching to mode 'Hold' is currently not possible
No valid global position estimate
[12:15:18.393 ] Critical: Switching to mode 'RTL' is currently not possible
No valid global position estimate
[12:15:16.488 ] Critical: Switching to mode 'RTL' is currently not possible
No valid global position estimate
[12:15:16.488 ] Critical: Switching to mode 'RTL' is currently not possible
No valid global position estimate
[12:15:16.488 ] Info: Pilot took over using sticks
[12:15:16.488 ] Info: Takeoff detected
[12:15:16.488 ] Info: Armed by RC (switch)
[12:15:16.488 ] Info: Disarmed by landing
[12:15:16.488 ] Info: Landing detected
[12:15:16.488 ] Critical: Switching to mode 'Hold' is currently not possible
No valid global position estimate
[12:15:16.488 ] Info: Pilot took over using sticks
[12:15:16.488 ] Info: Takeoff detected
[12:15:16.488 ] Info: Armed by RC (switch)
[12:15:16.297 ] Info: Using minimum takeoff altitude: 2.50 m
[12:15:16.297 ] Info: Using minimum takeoff altitude: 2.50 m
[12:15:16.297 ] Info: logging: opening log file 2025-11-17/19_54_55.ulg
[12:15:16.297 ] Info: Using minimum takeoff altitude: 2.50 m
[12:15:16.297 ] Info: logging: opening log file 2025-11-17/19_53_30.ulg
[12:15:15.039 ] Critical: Switching to mode 'RTL' is currently not possible
No valid global position estimate
[12:15:11.470 ] Info: Pilot took over using sticks
[12:15:07.340 ] Info: Takeoff detected
[12:15:07.340 ] Info: Armed by RC (switch)
[12:15:07.340 ] Info: Disarmed by landing
[12:15:07.340 ] Info: Landing detected
[12:15:07.339 ] Critical: Switching to mode 'Hold' is currently not possible
No valid global position estimate
[12:15:07.339 ] Info: Pilot took over using sticks
[12:15:07.339 ] Info: Takeoff detected
[12:15:07.339 ] Info: Armed by RC (switch)
[12:15:07.338 ] Info: Kill-switch disengaged
[12:15:07.158 ] Info: Using minimum takeoff altitude: 2.50 m
[12:15:02.686 ] Info: logging: opening log file 2025-11-17/19_54_55.ulg
[12:15:02.686 ] Info: Using minimum takeoff altitude: 2.50 m
[12:15:02.686 ] Info: logging: opening log file 2025-11-17/19_53_30.ulg
[12:15:02.607 ] Info: Armed by RC (switch)
[12:14:18.746 ] Info: Disarmed by landing
[12:14:18.534 ] Info: Landing detected
[12:13:47.472 ] Critical: Switching to mode 'Hold' is currently not possible
No valid global position estimate
[12:13:44.044 ] Info: Pilot took over using sticks
[12:13:40.189 ] Info: Takeoff detected
[12:13:37.149 ] Info: Armed by RC (switch)
[12:13:31.517 ] Info: Kill-switch disengaged
[12:13:29.244 ] Info: Kill-switch engaged
[12:13:16.937 ] Info: Disarmed by landing
[12:13:16.902 ] Info: Landing detected
[12:13:16.341 ] Info: Pilot took over using sticks
[12:13:16.336 ] Info: Takeoff detected
[12:13:16.331 ] Info: Armed by RC (switch)
[12:13:16.326 ] Info: Disarmed by landing
[12:13:16.322 ] Info: Landing detected
[12:13:16.317 ] Info: Pilot took over using sticks
[12:13:16.312 ] Info: Takeoff detected
[12:13:16.307 ] Info: Armed by RC (switch)
[12:13:16.302 ] Info: Disarmed by landing
[12:13:16.297 ] Info: Landing detected
[12:13:16.292 ] Info: Pilot took over using sticks
[12:13:16.287 ] Info: Takeoff detected
[12:13:16.281 ] Info: Armed by RC (switch)
[12:13:16.275 ] Info: Disarmed by landing
[12:13:16.268 ] Info: Using minimum takeoff altitude: 2.50 m
[12:13:16.261 ] Info: logging: opening log file 2025-11-17/19_53_5.ulg
[12:13:16.253 ] Info: Using minimum takeoff altitude: 2.50 m
[12:13:16.248 ] Info: logging: opening log file 2025-11-17/19_52_47.ulg
[12:13:16.241 ] Info: Using minimum takeoff altitude: 2.50 m
[12:13:16.225 ] Info: logging: opening log file 2025-11-17/19_52_29.ulg
[12:13:13.767 ] Info: Takeoff detected
[12:13:13.763 ] Info: Armed by RC (switch)
[12:13:13.759 ] Info: Disarmed by landing
[12:13:13.754 ] Info: Landing detected
[12:13:13.749 ] Info: Pilot took over using sticks
[12:13:13.745 ] Info: Takeoff detected
[12:13:13.740 ] Info: Armed by RC (switch)
[12:13:13.735 ] Info: Disarmed by landing
[12:13:13.729 ] Info: Landing detected
[12:13:13.724 ] Info: Pilot took over using sticks
[12:13:13.717 ] Info: Takeoff detected
[12:13:13.711 ] Info: Armed by RC (switch)
[12:13:13.703 ] Info: Disarmed by landing
[12:13:13.694 ] Info: Landing detected
[12:13:13.683 ] Info: Pilot took over using sticks
[12:13:12.160 ] Info: logging: opening log file 2025-11-17/19_53_5.ulg
[12:13:12.153 ] Info: Using minimum takeoff altitude: 2.50 m
[12:13:12.149 ] Info: logging: opening log file 2025-11-17/19_52_47.ulg
[12:13:12.144 ] Info: Using minimum takeoff altitude: 2.50 m
[12:13:12.139 ] Info: logging: opening log file 2025-11-17/19_52_29.ulg
[12:13:12.070 ] Info: Armed by RC (switch)
[12:12:58.777 ] Info: Disarmed by landing
[12:12:58.670 ] Info: Landing detected
[12:12:57.884 ] Info: Pilot took over using sticks
[12:12:57.388 ] Info: Takeoff detected
[12:12:57.388 ] Info: Armed by RC (switch)
[12:12:57.388 ] Info: Disarmed by landing
[12:12:57.388 ] Info: Landing detected
[12:12:57.388 ] Info: Pilot took over using sticks
[12:12:57.388 ] Info: Takeoff detected
[12:12:57.388 ] Info: Armed by RC (switch)
[12:12:57.388 ] Info: Disarmed by landing
[12:12:57.388 ] Info: Landing detected
[12:12:57.388 ] Info: Pilot took over using sticks
[12:12:57.388 ] Info: Takeoff detected
[12:12:57.387 ] Info: Armed by RC (switch)
[12:12:57.211 ] Info: Using minimum takeoff altitude: 2.50 m
[12:12:54.313 ] Info: logging: opening log file 2025-11-17/19_52_47.ulg
[12:12:54.313 ] Info: Using minimum takeoff altitude: 2.50 m
[12:12:54.313 ] Info: logging: opening log file 2025-11-17/19_52_29.ulg
[12:12:54.313 ] Info: Using minimum takeoff altitude: 2.50 m
[12:12:54.313 ] Info: logging: opening log file 2025-11-17/19_52_19.ulg
[12:12:54.254 ] Info: Armed by RC (switch)
[12:12:41.587 ] Info: Disarmed by landing
[12:12:41.454 ] Info: Landing detected
[12:12:40.913 ] Info: Pilot took over using sticks
[12:12:40.660 ] Info: Takeoff detected
[12:12:40.660 ] Info: Armed by RC (switch)
[12:12:40.659 ] Info: Disarmed by landing
[12:12:40.658 ] Info: Landing detected
[12:12:40.658 ] Info: Pilot took over using sticks
[12:12:40.658 ] Info: Takeoff detected
[12:12:40.658 ] Info: Armed by RC (switch)
[12:12:40.657 ] Info: Kill-switch disengaged
[12:12:35.914 ] Info: Armed by RC (switch)
[12:12:30.895 ] Info: Disarmed by landing
[12:12:30.783 ] Info: Landing detected
[12:12:30.049 ] Info: Pilot took over using sticks
[12:12:29.510 ] Info: Takeoff detected
[12:12:26.738 ] Info: Armed by RC (switch)
[12:12:25.307 ] Info: Kill-switch disengaged
[12:12:24.078 ] Info: Kill-switch engaged
[12:10:59.109 ] Info: Kill-switch disengaged
[12:10:57.503 ] Info: Disarmed by kill switch
[12:10:57.503 ] Critical: Kill-switch engaged
[12:10:57.124 ] Info: Pilot took over using sticks
[12:10:57.124 ] Info: Pilot took over using sticks
[12:10:57.124 ] Critical: Switching to mode 'Hold' is currently not possible
No valid global position estimate
[12:10:57.124 ] Critical: Switching to mode 'Hold' is currently not possible
No valid global position estimate
[12:10:57.124 ] Info: Pilot took over using sticks
[12:10:57.124 ] Info: Takeoff detected
[12:10:57.124 ] Info: Armed by RC (switch)
[12:10:57.124 ] Info: Disarmed by landing
[12:10:57.124 ] Info: Landing detected
[12:10:57.124 ] Info: Pilot took over using sticks
[12:10:57.124 ] Info: Takeoff detected
[12:10:57.124 ] Info: Armed by RC (switch)
[12:10:57.124 ] Critical: Arming denied: switch to manual mode first
[12:10:57.122 ] Info: Using minimum takeoff altitude: 2.50 m
[12:10:57.122 ] Info: Using minimum takeoff altitude: 2.50 m
[12:10:57.122 ] Info: Using minimum takeoff altitude: 2.50 m
[12:10:57.122 ] Info: logging: opening log file 2025-11-17/19_49_29.ulg
[12:10:57.122 ] Info: Using minimum takeoff altitude: 2.50 m
[12:10:57.122 ] Info: logging: opening log file 2025-11-17/19_49_5.ulg
[12:10:48.048 ] Info: Pilot took over using sticks
[12:10:41.967 ] Critical: Switching to mode 'Hold' is currently not possible
No valid global position estimate
[12:10:41.967 ] Critical: Switching to mode 'Hold' is currently not possible
No valid global position estimate
[12:10:41.967 ] Info: Pilot took over using sticks
[12:10:41.967 ] Info: Takeoff detected
[12:10:41.967 ] Info: Armed by RC (switch)
[12:10:41.967 ] Info: Disarmed by landing
[12:10:41.967 ] Info: Landing detected
[12:10:41.967 ] Info: Pilot took over using sticks
[12:10:41.967 ] Info: Takeoff detected
[12:10:41.967 ] Info: Armed by RC (switch)
[12:10:41.967 ] Critical: Arming denied: switch to manual mode first
[12:10:36.926 ] Info: Using minimum takeoff altitude: 2.50 m
[12:10:36.926 ] Info: Using minimum takeoff altitude: 2.50 m
[12:10:36.926 ] Info: logging: opening log file 2025-11-17/19_49_29.ulg
[12:10:36.926 ] Info: Using minimum takeoff altitude: 2.50 m
[12:10:36.925 ] Info: logging: opening log file 2025-11-17/19_49_5.ulg
[12:09:49.450 ] Critical: Switching to mode 'Hold' is currently not possible
No valid global position estimate
[12:09:44.699 ] Info: Pilot took over using sticks
[12:09:38.982 ] Info: Takeoff detected
[12:09:38.982 ] Info: Armed by RC (switch)
[12:09:38.982 ] Info: Disarmed by landing
[12:09:38.982 ] Info: Landing detected
[12:09:38.982 ] Info: Pilot took over using sticks
[12:09:38.982 ] Info: Takeoff detected
[12:09:38.982 ] Info: Armed by RC (switch)
[12:09:38.982 ] Critical: Arming denied: switch to manual mode first
[12:09:38.816 ] Info: Using minimum takeoff altitude: 2.50 m
[12:09:35.912 ] Info: logging: opening log file 2025-11-17/19_49_29.ulg
[12:09:35.912 ] Info: Using minimum takeoff altitude: 2.50 m
[12:09:35.912 ] Info: logging: opening log file 2025-11-17/19_49_5.ulg
[12:09:35.842 ] Info: Armed by RC (switch)
[12:09:20.407 ] Info: Disarmed by landing
[12:09:20.406 ] Info: Landing detected
[12:09:18.821 ] Info: Pilot took over using sticks
[12:09:17.483 ] Info: Takeoff detected
[12:09:17.483 ] Info: Armed by RC (switch)
[12:09:17.483 ] Critical: Arming denied: switch to manual mode first
[12:09:12.580 ] Info: Armed by RC (switch)
[12:09:04.564 ] Critical: Arming denied: switch to manual mode first
[12:01:39.430 ] Critical: Manual control lost
[11:40:15.660 ] Info: Disarmed by landing
[11:40:15.557 ] Info: Landing detected
[11:40:12.945 ] Critical: Switching to mode 'Hold' is currently not possible
- No valid local position estimate
- No valid global position estimate

[11:40:09.043 ] Critical: Switching to mode 'Hold' is currently not possible
- No valid local position estimate
- No valid global position estimate

[11:39:59.600 ] Info: Takeoff detected
[11:39:59.600 ] Info: Armed by RC (switch)
[11:39:56.675 ] Info: Armed by RC (switch)
[11:36:22.687 ] Critical: Arming denied: switch to manual mode first
[11:36:20.623 ] Critical: Arming denied: switch to manual mode first
[11:17:01.952 ] Info: Kill-switch disengaged
[11:17:01.009 ] Info: Kill-switch engaged
[11:14:42.859 ] Info: Disarmed by landing
[11:14:42.658 ] Info: Landing detected
[11:13:49.742 ] Info: Takeoff detected
[11:13:49.742 ] Info: Armed by RC (switch)
[11:13:43.892 ] Info: Armed by RC (switch)
[11:11:52.513 ] Info: Manual control regained after 2.3 s
[11:11:50.416 ] Critical: Manual control lost
[11:11:14.269 ] Info: Kill-switch disengaged
[11:11:14.198 ] Info: Kill-switch engaged
[11:11:14.025 ] Info: Kill-switch disengaged
[11:11:13.898 ] Info: Kill-switch engaged
[11:11:13.743 ] Info: Kill-switch disengaged
[11:11:13.677 ] Info: Kill-switch engaged
[11:11:11.927 ] Info: Kill-switch disengaged
[11:11:11.733 ] Info: Kill-switch engaged
[11:09:52.656 ] Info: Disarmed by auto preflight disarming
[11:09:49.570 ] Critical: Switching to AUTO_LAND is currently not available ... 
[11:09:48.548 ] Critical: Switching to mode 'Land' is currently not possible
No valid local position estimate
[11:09:48.341 ] Critical: Switching to AUTO_LAND is currently not available ... 
[11:09:47.211 ] Critical: Switching to mode 'Land' is currently not possible
No valid local position estimate
[11:09:46.905 ] Critical: Switching to AUTO_LAND is currently not available ... 
[11:09:45.836 ] Critical: Switching to mode 'Land' is currently not possible
No valid local position estimate
[11:09:40.659 ] Info: Armed by RC (switch)
[11:09:32.638 ] Info: Armed by RC (switch)
[11:04:16.115 ] Critical: Manual control lost
[11:01:26.781 ] Info: Kill-switch disengaged
[11:01:12.550 ] Info: Disarmed by kill switch
[11:01:12.549 ] Critical: Kill-switch engaged
[11:00:55.549 ] Info: Takeoff detected
[11:00:55.549 ] Info: Armed by RC (switch)
[11:00:55.549 ] Info: Disarmed by RC (switch)
[11:00:55.549 ] Info: Armed by RC (switch)
[11:00:55.549 ] Info: Disarmed by landing
[11:00:55.549 ] Info: Landing detected
[11:00:55.549 ] Info: Takeoff detected
[11:00:55.549 ] Info: Armed by RC (switch)
[11:00:55.549 ] Info: Disarmed by auto preflight disarming
[11:00:55.549 ] Info: Armed by RC (switch)
[11:00:52.015 ] Info: logging: opening log file 2025-11-17/19_53_55.ulg
[11:00:52.015 ] Info: logging: opening log file 2025-11-17/19_53_54.ulg
[11:00:52.015 ] Info: logging: opening log file 2025-11-17/19_53_51.ulg
[11:00:52.015 ] Info: logging: opening log file 2025-11-17/19_53_27.ulg
[11:00:51.948 ] Info: Armed by RC (switch)
[11:00:51.887 ] Info: Disarmed by RC (switch)
[11:00:51.887 ] Info: Armed by RC (switch)
[11:00:51.887 ] Info: Disarmed by landing
[11:00:51.887 ] Info: Landing detected
[11:00:51.887 ] Info: Takeoff detected
[11:00:51.887 ] Info: Armed by RC (switch)
[11:00:51.887 ] Info: Disarmed by auto preflight disarming
[11:00:51.887 ] Info: Armed by RC (switch)
[11:00:50.323 ] Info: logging: opening log file 2025-11-17/19_53_54.ulg
[11:00:50.323 ] Info: logging: opening log file 2025-11-17/19_53_51.ulg
[11:00:50.323 ] Info: logging: opening log file 2025-11-17/19_53_27.ulg
[11:00:50.305 ] Info: Armed by RC (switch)
[11:00:48.737 ] Info: Disarmed by landing
[11:00:48.511 ] Info: Landing detected
[11:00:47.907 ] Info: Takeoff detected
[11:00:47.907 ] Info: Armed by RC (switch)
[11:00:47.907 ] Info: Disarmed by auto preflight disarming
[11:00:47.906 ] Info: Armed by RC (switch)
[11:00:47.904 ] Info: logging: opening log file 2025-11-17/19_53_51.ulg
[11:00:47.904 ] Info: logging: opening log file 2025-11-17/19_53_27.ulg
[11:00:47.837 ] Info: Armed by RC (switch)
[11:00:44.015 ] Info: Disarmed by auto preflight disarming
[11:00:44.015 ] Info: Armed by RC (switch)
[11:00:24.090 ] Info: Armed by RC (switch)
[10:59:33.856 ] Info: Kill-switch disengaged
[10:59:32.507 ] Info: Kill-switch engaged
[10:53:59.557 ] Critical: Manual control lost
[10:52:17.436 ] Critical: Manual control lost
[10:49:59.340 ] Critical: Manual control lost
[10:45:29.145 ] Info: Kill-switch disengaged
[10:45:28.487 ] Info: Kill-switch engaged
[10:45:15.907 ] Info: Kill-switch disengaged
[10:45:15.651 ] Info: Kill-switch engaged
[10:45:15.205 ] Info: Kill-switch disengaged
[10:45:15.090 ] Info: Kill-switch engaged
```