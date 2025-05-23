# Universal Powerline Bus + Hubitat Integration

The Universal Powerline Bus (UPB) is a communication protocol used for home automation and building control. It enables devices to communicate over the existing powerline infrastructure, eliminating the need for additional wiring. UPB is a robust, reliable, and scalable technology designed for applications such as lighting control, HVAC management, and appliance integration. Through testing, field trials, and residential installations, UPB has been proven to be greater than 99.9% reliable.

Connecting your existing UPB investment allows you to benefit from modern features like Google Assistant, Apple HomeKit, and Amazon Alexa.

## Minimum Requirements

1. Hubitat Elevation® Model C-7 or C-8 controller [Click here to purchase for Hubitat Elevation](https://hubitat.com)
2. Pulseworx PIM-U Powerline Interface Module [Click here to purchase PIM-U](https://pcswebstore.com/products/pulseworx-powerline-interface-module-usb)
3. Linux device running net2ser eg. Raspbery Pi [Click here to purchase Raspberry Pi](https://www.raspberrypi.com/products/raspberry-pi-5)
4. Download the UPBeat Hubitat Drivers [Click here to download driver bundle](https://github.com/UPBeat-Automation/UPBeat-Hubitat/releases)

## Recommended Setup for Power Over Ethernet (POE)
1. Hubitat Elevation® Model C-7 or C-8 controller [Click here to purchase for Hubitat Elevation](https://hubitat.com)
2. POE micro USB Adapter for Model C-7 [Click here to purchase micro USB POE adapter](https://www.amazon.com/dp/B01MDLUSE7) 
3. Pulseworx PIM-U Powerline Interface Module [Click here to purchase PIM-U](https://pcswebstore.com/products/pulseworx-powerline-interface-module-usb)
4. Linux device running net2ser eg. Raspbery Pi [Click here to purchase Raspberry Pi](https://www.raspberrypi.com/products/raspberry-pi-5)
5. Rapberry Pi Case [Click here to buy official Pi 5 case](https://www.digikey.com/en/products/detail/raspberry-pi/SC1160/21658256)
6. Raspberry Pi POE Hat [Click here to purchase Raspberry Pi POE Hat](https://www.amazon.com/dp/B0D7SDGXKL)
7. Download the UPBeat Hubitat Drivers [Click here to download driver bundle](https://github.com/UPBeat-Automation/UPBeat-Hubitat/releases)

## Installing Ser2Net for Ubuntu / Raspberry Pi

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
   
![image](https://github.com/user-attachments/assets/089a4e92-1e42-4d09-9b16-2b4ff1081f9a)

## Installing Hubitat Drivers

1. Download the drivers bundle from [releases](https://github.com/UPBeat-Automation/UPBeat-Hubitat/releases)
   ![image](https://github.com/user-attachments/assets/97423b7e-5bc6-474e-8ad6-54f60a3c5d81)

3. Navigate to your Hubitat Controller's web interface and go to the "FOR DEVELOPERS" --> Bundles
   
   ![image](https://github.com/user-attachments/assets/c1379932-5205-41d8-a437-0c6e5c2b718f)
4. Import the "UPBeatUniversalPowerlineBusIntegration.zip" into your Hubitat controller.
   
   ![image](https://github.com/user-attachments/assets/b5b64246-5db8-4f22-b683-33d23e6fbc83)

5. Once the import is completed, you should see the following.

   ![image](https://github.com/user-attachments/assets/e33a10c9-53ac-45b8-ba49-7cd0134667ff)

## Configuring the UPBeat App

1. Navigate to your Hubitat Controller's web interface and go to the Apps section.

   ![image](https://github.com/user-attachments/assets/12be96d6-4bce-4c85-94cb-2782b714fbaa)

2. Click "Add user app" and click UPBeat App.

   ![image](https://github.com/user-attachments/assets/d4b3d667-6f3c-4b8b-b22c-8504ab097446)

3. Click "Done" on the app page.

   ![image](https://github.com/user-attachments/assets/6dfefaac-6689-49dc-af4e-30dca42ec943)

## Configuring the UPBeat Powerline Interface Module
1. Navigate to your Hubitat Controller's web interface and go to the Devices section.
   
   ![image](https://github.com/user-attachments/assets/763b28e0-800b-471c-afca-32840cbc95d0)
3. Edit the UPB Powerline Interface Module device, goto the Preferences tab. Set the IP and port of your ser2net device from earlier.
   
   ![image](https://github.com/user-attachments/assets/cc3204af-451b-4642-b326-435f26a4a680)
5. Save, the setting and go to the Commands tab. You should see the following.
   
   ![image](https://github.com/user-attachments/assets/450e4221-dc2d-480b-9560-adf6cdf72cb5)

   The PIM driver is a raw socket driver, sometimes you will see the following status.  
   ![image](https://github.com/user-attachments/assets/2329c3b1-9a1f-4628-8af3-ff6b43fb8c5c)

   It's completely normal and comes from the socket driver when no data arrives in a minute.

## Adding devices manually
1. Navigate to your Hubitat Controller's web interface and go to the Apps section. Click on UPBeat App.
   
   ![image](https://github.com/user-attachments/assets/b7f712b3-b726-4d3f-9f91-9e2f3d58149b)

3. Click on the "Manually Add Device", select a device type. as shown below.

   ![image](https://github.com/user-attachments/assets/ee80ec92-e007-4c93-8d0b-dd6d60421cac)

4. Set the Name, Voice Name, UPB Network Id, and UPB Device Id, click Next.

   ![image](https://github.com/user-attachments/assets/536bd691-28e7-45c4-a5b8-119d39667865)

5. Click the Go to Device Page button.

   ![image](https://github.com/user-attachments/assets/090cdd8b-d502-40a3-93aa-dbb08c3f0b51)

6. You should now be able to control your device.

## Adding devices via UpStart UPE import

1. Navigate to your Hubitat Controller's web interface and go to the Apps section. Click on UPBeat App.
   
   ![image](https://github.com/user-attachments/assets/5648441b-e07f-4999-bb47-386d4efd4581)

2. Select Bulk Import and paste UPE file contents. Then click Next.

   ![image](https://github.com/user-attachments/assets/9b0089fe-680c-40d0-b4c1-556fe02a78d2)

   Review the import results, and click Next. 

   ![image](https://github.com/user-attachments/assets/6ba492c0-0c04-4865-8f7e-fce7e7641d03)

   You are ready to go... 🥇

   ![image](https://github.com/user-attachments/assets/616afa43-5e8e-46a7-98ed-12c7ac099878)


## Limitations

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
