My printer came with the new v4.2.2 motherboard as evident from the photo as well as have the ARM processor into it. For updation.

### Compiling from source-code

---

1. Go to marlin github rep  : [https://github.com/MarlinFirmware/Marlin](https://github.com/MarlinFirmware/Marlin)
2. Choose the branch. I chose the bugfix-2.0.x
3. Download all the zip files. 
4. Also download the configuration : [https://github.com/MarlinFirmware/Configurations](https://github.com/MarlinFirmware/Configurations). Make sure to choose same branch as chose for the original source code. 
5. Install the platform.ini and marlin plugin in vscode.
6. Inside Configuration —> Creality —> Ender 3 —> Crealityv422, copy all those files to Marlin-bugfix-2.0.x/Marlin and replace all of them.
7. Edit the **platform.ini**

    ```jsx
    default_envs = STM32F103RET6_creality
    ```

    Edit the **Marlin/Configuration.h**

    ```jsx
    */
    #define SERIAL_PORT 1

    /**
     * Select a secondary serial port on the board to use for communication with the host.
     * Currently Ethernet (-2) is only supported on Teensy 4.1 boards.
     * :[-2, -1, 0, 1, 2, 3, 4, 5, 6, 7]
     */
    #define SERIAL_PORT_2 3
    ```

    ```jsx
    #define CR10_STOCKDISPLAY
    #if ENABLED(CR10_STOCKDISPLAY)
      #define RET6_12864_LCD  // Specific to the SoC (can either be RET / VET)
    #endif
    ```

8. Compile the source-code and should see a success like this

    ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/38066b64-5866-481a-8ba2-95944b7e0608/Screenshot_from_2021-04-02_14-28-34.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/38066b64-5866-481a-8ba2-95944b7e0608/Screenshot_from_2021-04-02_14-28-34.png)

9. The main firmware file is in .pio/build/firmware-<number>-<number>.bin. Copy and paste than into root directory of SD card.
10. Turn off the printer, insert SD card with new .bin firmware and the printer should automatically update the firmware.

### BL-Touch

---

1. In configuration.hh, enable the BL-touch conditional. Switch it back to comment if no bl touch will be connected.

    ```jsx
    #define BLTOUCH
    ```

Also have to enable the z probe, and if not turned on, automatically compiler will raise error and advise to turn on the other necessary settings. 

2. 

```jsx
comment
// #define Z_MIN_PROBE_USES_Z_MIN_ENDSTOP_PIN

uncomment
#define USE_PROBE_FOR_Z_HOMING

#define Z_MIN_PROBE_PIN PB1
```

### Front-boot screen

---

1. Edit the _Bootscreen.h. Replace the bitmap custom_start_bmp[] PROGMEM with your customer image. Also possible to generate one here : [https://marlinfw.org/tools/u8glib/converter.html](https://marlinfw.org/tools/u8glib/converter.html)

### Resources used

---

[https://www.youtube.com/watch?v=kFRy_5lh2IQ](https://www.youtube.com/watch?v=kFRy_5lh2IQ)

[Creality Ender 3/3 Pro Firmware | V4.2.X Board - TH3D Studio LLC](https://support.th3dstudio.com/hc/downloads/unified-2-firmware/creality/creality-ender-3-3-pro-ender-5-5-pro-firmware-v4-2-x-board/)

[Download | Creality 3D](https://www.creality.com/download)

[Creality 32 bit V4 board guide - Ender 3 V2, BLtouch & more](https://www.youtube.com/watch?v=neS7lB7fCww)

[Beginner guide to editing Marlin firmware - step by step - UPDATE IN DESCRIPTION](https://www.youtube.com/watch?v=J9vxJT5Tgh4)
