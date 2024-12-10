## Universal Powerline Bus + Hubitat Integration

### Requirements

1. Hubitat Elevation® Model C-7 or C-8 controller [Click here to purchase for Hubitat Elevation](https://hubitat.com)
3. GridConnect Serial to Ethernet adapter or Linux device running net2ser. [Click here to purchase GridConnect GC-ND-POE-DCE](https://www.gridconnect.com/products/netdirect-serial-to-power-over-ethernet-poe-cable)
4. Download the UPBeat UI
5. Download the UPBeat Hubitat Drivers
   
### Installing Ser2Net for Ubuntu / Raspberry Pi



#### Modify the /etc/ser2net.yaml to have the correct IP and serial device for your PIM module

The IP address should be the IP of the device that is running Ser2Net and port in the example below is set to 4999, but you can configure a different port. Additionally, the Powerline Interface Module (PIM) will need to be connected to the Linux device. You will need to make sure that the correct /dev/tty* is used in your configuration file. 

```yaml
connection: &UPBPIM
    accepter: tcp,<IP Address>,<Port> # Change the IP and port to your liking
    enable: on
    options:
      kickolduser: true
      telnet-brk-on-sync: false
    connector: serialdev,
              <Device>, # Set this to the correct serial device where the PIM is connected.
              4800n81,local
```

#### Raspberry Pi example with USB to Serial adapter.
```yaml
connection: &UPBPIM
    accepter: tcp,192.168.1.5,4999
    enable: on
    options:
      kickolduser: true
      telnet-brk-on-sync: false
    connector: serialdev,
              /dev/ttyUSB0,
              4800n81,local
```
