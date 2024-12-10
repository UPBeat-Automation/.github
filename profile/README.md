## Universal Powerline Bus + Hubitat Integration

### Requirements

1. Hubitat Elevation® Model C-7 or C-8 controller [Click here to purchase for Hubitat Elevation](https://hubitat.com)
3. GridConnect Serial to Ethernet adapter or Linux device running net2ser. [Click here to purchase GridConnect GC-ND-POE-DTE Male](https://www.gridconnect.com/products/netdirect-serial-to-power-over-ethernet-poe-cable)
4. Download the UPBeat UI
5. Download the UPBeat Hubitat Drivers
   
### Installing Ser2Net for Ubuntu / Raspberry Pi

1. Use apt to install Ser2Net, you should be able to cut and paste the following commands:

```bash
sudo apt update
sudo apt install ser2net
```


2. As root, using a text editor, modify the /etc/ser2net.yaml.
   The IP address should be the IP of the device that is running Ser2Net and port in the example below is set to 4999, but you can configure a different port. Additionally, the Powerline Interface Module (PIM) will need to be connected to the Linux device. You will need to make sure that the correct /dev/tty* is used in your configuration file. 

#### Raspberry Pi example with USB to Serial adapter.
```yaml
connection: &UPBPIM
    accepter: tcp,192.168.1.5,4999 # Change the IP (192.168.1.5) to the current system IP and port (4999) can remain the same or be changed
    enable: on
    options:
      kickolduser: true
      telnet-brk-on-sync: false
    connector: serialdev,
              /dev/ttyUSB0, # The device needs to match where the PIM is attached. 
              4800n81,local
```
