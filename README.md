# pikvm-ezcoo-gpio-labels
Fix proper labeling for Ezcoo 4-way HDMI splitter on a PiKVM (model ‎EZ-SW41HA-KVMU3L but presumably other 4-port models work as well.)

With the EzCoo 4-way splitter the labels don't seem to populate properly with the default instructions. Here's a working config tested in configuration with the generic Geekworm KVM-A3 Kit for Raspberry Pi 4 Open Source KVM Over IP (from Amazon.co.uk). Works great!

File: /etc/kvmd/override.conf
```
kvmd:
    gpio:
        view:
            header:
                title: Devices
            table:
                - ["#Device 1", ch0_led, ch0_button] # Note the hash sign prefix matters!
                - ["#Device 2", ch1_led, ch1_button] # Note the hash sign prefix matters!
                - ["#Device 3", ch2_led, ch2_button] # Note the hash sign prefix matters!
                - ["#Device 4", ch3_led, ch3_button] # Note the hash sign prefix matters!
        drivers:
            ez:
                type: ezcoo
                protocol: 2
                device: /dev/ttyUSB0
        scheme:
            ch0_led:
                driver: ez
                pin: 0
                mode: input
            ch1_led:
                driver: ez
                pin: 1
                mode: input
            ch2_led:
                driver: ez
                pin: 2
                mode: input
            ch3_led:
                driver: ez
                pin: 3
                mode: input
            ch0_button:
                driver: ez
                pin: 0
                mode: output
                switch: false
            ch1_button:
                driver: ez
                pin: 1
                mode: output
                switch: false
            ch2_button:
                driver: ez
                pin: 2
                mode: output
                switch: false
            ch3_button:
                driver: ez
                pin: 3
                mode: output
                switch: false

```
