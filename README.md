**Overview:**\
This Python script designed to:

Display the internal IP address of your Raspberry Pi on an OLED screen.\
Send an email notification when the internal IP changes, providing the new IP.\
The OLED screen is managed via Adafruit's SSD1306 library, and emails are sent using the SMTP protocol. The IP address is monitored, stored, and compared against the last known IP to trigger an email alert if a change is detected.

**Hardware:**\ 
Adafruit PiOLED - 128x32 Monochrome OLED\ 
I2C connections (SCL, SDA)\

**Software:**\ 
Virtual environment for package management:     
    -adafruit-circuitpython-ssd1306\
    -Pillow\
    -smtplib\
    -subprocess

**Setup Instructions:**\ 

1. Create Necessary Directories and Files 
```
mkdir ~/rpi_ip
cd ~/rpi_ip
touch last_ip.txt credentials.txt
```