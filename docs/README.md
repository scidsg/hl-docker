# Installation Guide

## Raspberry Pi, Tor-Only Install

### Requirements
- **Hardware:** [Raspberry Pi 4](https://www.amazon.com/Raspberry-Model-2019-Quad-Bluetooth/dp/B07TC2BK1X/?&_encoding=UTF8&tag=scidsg-20&linkCode=ur2&linkId=ee402e41cd98b8767ed54b1531ed1666&camp=1789&creative=9325)/[3B+](https://www.amazon.com/ELEMENT-Element14-Raspberry-Pi-Motherboard/dp/B07P4LSDYV/?&_encoding=UTF8&tag=scidsg-20&linkCode=ur2&linkId=d76c1db453c42244fe465c9c56601303&camp=1789&creative=9325)
- **Power:** [Raspberry Pi USB-C Power Supply](https://www.amazon.com/Raspberry-Pi-USB-C-Power-Supply?&_encoding=UTF8&tag=scidsg-20&linkCode=ur2&linkId=1b23995f6048ad84182dca1f160656e9&camp=1789&creative=9325)
- **Storage:** [Micro SD Card](https://www.amazon.com/SanDisk-128GB-MicroSDXC-Memory-Adapter/?&_encoding=UTF8&tag=scidsg-20&linkCode=ur2&linkId=fd8f40cfc6e84e328e3246af7159eb40&camp=1789&creative=9325)
- **SD Card Adapter:** [SD Card Reader](https://www.amazon.com/SanDisk-MobileMate-microSD-Card-Reader?&_encoding=UTF8&tag=scidsg-20&linkCode=ur2&linkId=40c1d3e78e132a951b46e61aab13e4e7&camp=1789&creative=9325) 
- **OS:** Raspberry Pi OS (64-bit)
- **Display** (Optional): [Waveshare 2.7" e-Paper display](https://www.amazon.com/2-7inch-HAT-Resolution-Electronic-Communicating/dp/B075FQKSZ9/?&_encoding=UTF8&tag=scidsg-20&linkCode=ur2&linkId=6963f1303b9d2b8ade8f92f37f2fda26&camp=1789&creative=9325)
- (👆 Affiliate links)

### Step 1: Install Raspberry Pi OS
1. Download and open the official Raspberry Pi Imager: https://www.raspberrypi.com/software/
2. Click _Choose OS > Raspberry Pi OS (other) > Raspberry Pi OS (64-bit)_.
3. If you have an SD card slot on your computer, insert your card. Otherwise, plug your adapter into a USB port and insert your card. 
4. Next, click Choose Storage and select your micro SD card.
5. Before writing the operating system to the card, click the Settings button in the bottom-right of the window.
   - Enable SSH and create a strong password.
   - Add your Wi-Fi information.
   - Adjust other settings as desired.
6. Click "Write".

### Step 2: Log in to your Pi

#### Boot Up Your Pi
1. Insert your SD card into the Raspberry Pi. You'll find the card slot on the bottom of the board, opposite the ethernet ports.
2. Plug it in using your new power supply.

#### Router Settings

1. To find your Pi's IP address after booting up, go to your router's admin settings and look for your connected devices. Your device should be named "raspberrypi."
2. Take note of its IP address. Its format might look like "192.168.0.4."
3. (_Optional, but recommended_) Next, look for "Address Reservations" in your router settings. It may also be called "Static IP Addresses." Sometimes, when your router or device reboots, your Pi will get assigned a different IP address. We want to assign it an IP so you can have a predictable address in case you need to log back into your Pi. Assign it the IP address it currently has and give it a descriptive name.
   - For **Netgear routers**, try the _Advanced tab > Setup > LAN Setup > Address Reservations > Add_.
   - For **TP-Link routers**, try _Advanced > DHCP Server > Address Reservation > Add_.
   - All routers are different, so look at the manufacturer's instructions if you can't find the settings.

#### Raspberry Pi   
1. Now that you've found your IP address, open a Terminal on your computer and log in to your Pi using SSH:
   
   ```
   ssh pi@<IP>
   ```

### Step 3: Install Hush Line

1. We'll install Hush Line as root:
   
   ```
   sudo su
   ```

2. To start the installation process, execute the following command:

   ```
   curl -sSL https://install.hushline.app | bash
   ```

### Step 4: Email Notifications

1. You'll need an SMTP-compatible email service to receive tip notifications. We're using Gmail in our example and need the following information:
- Gmail address
- SMTP address: smtp.gmail.com
- [App password](https://support.google.com/accounts/answer/185833?hl=en)
- Port: 465
- If our Gmail address is myburneremail@gmail.com, email notifications will be delivered to that Gmail account.
  - Remember that you can forward messages to any address in your Gmail settings.

### Step 5: Create And Add Your PGP Key

#### MacOS Instructions

1. Download and install [GPG Suite](https://gpgtools.org/).
2. Open GPG Keychain.
3. Click "New" at the top of the window.
4. Create a key for the email address of your tip line. _You do not have to use your notification email address_. Science & Design uses "tips@scidsg.org" for our purposes. It's critical to enter an email address you own that can receive a confirmation email.
5. After creating your key, choose to upload it to a public keyserver. You'll need to confirm your email address before it finishes uploading. 
6. On the appropriate prompt during installation, enter the address of your uploaded key. For example, for our key seen at https://keys.openpgp.org/search?q=demo@scidsg.org, we would enter https://keys.openpgp.org/vks/v1/by-fingerprint/D278DD437B275C8668989A4B425C6C74405C3EB1. 

### Step 6: Access Hush Line

1. When the installation completes, you'll see your Hush Line address:
   
   ```
   ✅ Installation complete!
                                               
   Hush Line is a product by Science & Design. 
   Learn more about us at https://scidsg.org.
   Have feedback? Send us an email at hushline@scidsg.org.

   ● Hush Line is running
   http://vfalkrrucjb7pztjskfumnqytpze5iimu4i2t2ygwv6ntylvylt2flad.onion
   ```
3. To access your tip line, download [Tor Browser](https://torproject.org/download) and enter the onion address above.

### Step 7: Add An E-Paper Display (optional)

1. We support the Waveshare 2.7" e-paper display. Attach the display to your Pi's GPIO pins with your Pi powered off. Make sure it's seated securely.
2. Next, execute the following command:
   
   ```
   curl -sSL https://raw.githubusercontent.com/scidsg/hushline/main/scripts/waveshare-2_7in-eink-display.sh | bash
   ```
4. Follow the prompts to enable the SPI interface.
5. When the installation completes, the device will reboot. You'll see the Hush Line splash screen, followed by information about your tip line. It will look like this:
   
   <img width="350" alt="Group 27" src="https://github.com/scidsg/hushline/assets/28545431/8fd840d2-c2b9-4ba3-b0f8-bbe105c1baa2">
