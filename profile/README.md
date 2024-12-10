## Universal Powerline Bus + Hubitat Integration

The Universal Powerline Bus (UPB) is a communication protocol used for home automation and building control. It enables devices to communicate over the existing powerline infrastructure, eliminating the need for additional wiring. UPB is a robust, reliable, and scalable technology designed for applications such as lighting control, HVAC management, and appliance integration. Through testing, field trials, and residential installations, UPB has been proven to be greater than 99.9% reliable.

Connecting your existing UPB investment allows you to benefit from modern features like Google Assistant, Apple HomeKit, and Amazon Alexa.

### Coming Soon

The client code, drivers, and documentation will be released soon. Feel free to reach out in the meantime. 

### Requirements

1. Hubitat Elevation® Model C-7 or C-8 controller [Click here to purchase for Hubitat Elevation](https://hubitat.com)
2. Pulseworx PIM-R Powerline Interface Module RS232 [Click here to purchase PIM-R](https://pcswebstore.com/products/pulseworx-powerline-interface-module-rs232)
3. GridConnect Serial to Ethernet adapter or Linux device running net2ser. [Click here to purchase GridConnect GC-ND-POE-DTE Male](https://www.gridconnect.com/products/netdirect-serial-to-power-over-ethernet-poe-cable).
   - Be sure to buy the Male adapter as this can plug directly into the PIM.
5. Download the UPBeat UI
6. Download the UPBeat Hubitat Drivers
   
### Installing Ser2Net for Ubuntu / Raspberry Pi

1. Use apt to install Ser2Net, you should be able to cut and paste the following commands:

```bash
sudo apt update
sudo apt install ser2net
```


2. As root, using a text editor, modify the /etc/ser2net.yaml.
   The IP address should be the IP of the device that is running Ser2Net and port in the example below is set to 4999, but you can configure a different port. Additionally, the Powerline Interface Module (PIM) will need to be connected to the Linux device. You will need to make sure that the correct /dev/tty* is used in your configuration file. 

#### Raspberry Pi example with USB to Serial adapter:
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
