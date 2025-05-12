## Universal Powerline Bus + Hubitat Integration

The Universal Powerline Bus (UPB) is a communication protocol used for home automation and building control. It enables devices to communicate over the existing powerline infrastructure, eliminating the need for additional wiring. UPB is a robust, reliable, and scalable technology designed for applications such as lighting control, HVAC management, and appliance integration. Through testing, field trials, and residential installations, UPB has been proven to be greater than 99.9% reliable.

Connecting your existing UPB investment allows you to benefit from modern features like Google Assistant, Apple HomeKit, and Amazon Alexa.

### Coming Soon

The client code, drivers, and documentation will be released soon. Feel free to reach out in the meantime. 

### Requirements

1. Hubitat Elevation® Model C-7 or C-8 controller [Click here to purchase for Hubitat Elevation](https://hubitat.com)
2. Pulseworx PIM-U Powerline Interface Module [Click here to purchase PIM-U](https://pcswebstore.com/products/pulseworx-powerline-interface-module-usb)
3. Linux device running net2ser eg. Raspbery Pi [Click here to purchase Raspberry Pi](https://www.raspberrypi.com/products/raspberry-pi-5)
4. Download the UPBeat UI (Optional) - Still in development
5. Download the UPBeat Hubitat Drivers

### Installing Ser2Net for Ubuntu / Raspberry Pi

1. Raspbian (Raspberry Pi OS Lite) [Installing Raspberry Pi OS](https://www.raspberrypi.com/documentation/computers/getting-started.html)
2. Once installed, use apt to install Ser2Net, you should be able to cut and paste the following commands:

```bash
sudo apt update
sudo apt install ser2net
```

3. As root, using a text editor, modify the /etc/ser2net.yaml.
   The IP address should be the IP of the device that is running Ser2Net and port in the example below is set to 4999, but you can configure a different port. Additionally, the Powerline Interface Module (PIM) will need to be connected to the Linux device. 

#### Raspberry Pi example with Pulseworx PIM-U Powerline Interface Module:
```yaml
connection: &UPBPIM
    # Change the IP (192.168.1.5) to the current system IP and port (4999) can remain the same or be changed
    accepter: tcp,192.168.1.5,4999 
    enable: on
    options:
      kickolduser: true
      telnet-brk-on-sync: false
    connector: serialdev,
              /dev/ttyUSB0, # The device needs to match where the PIM is attached. 
              4800n81,local
```

4. Once you have saved the changes to the /etc/ser2net.yaml file you will need to restart the ser2net service. Using the following commands.
```
sudo service ser2net stop
sudo service ser2net start
```

5. Check the service status using `sudo service ser2net status` you should see somthing like shown below.
   
![image](https://github.com/user-attachments/assets/11b53c26-bd45-491b-8afd-17a4e26dad7a)

#### Installing Hubitat Drivers

1. Download the drivers bundle.

### Limitations

The UPBeat UI is able to store ane parse the complete UPE file, however; some device types are not currently supported, please see the list below for more information: 

- 0 = Other (Unsupported)
- 1 = Keypad (Unsupported)
- 2 = Switch (On/Off/Dim)
- 3 = Module (On/Off/Dim)
- 4 = Input Module (Unsupported)
- 5 = Input-Output Module (Unsupported)
- 6 = VPM (Unsupported)
- 7 = VHC (Unsupported)
- 8 = Thermostat (Unsupported)
- 9 = XPW (Unsupported)
- 10 = RFI (Unsupported)

We hope to grow device support with the help of the community and other developers. 
