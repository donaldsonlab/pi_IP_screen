**Overview:**  
This Python script designed to:  

Display the internal IP address of your Raspberry Pi on an OLED screen.  
Send an email notification when the internal IP changes, providing the new IP.  
The OLED screen is managed via Adafruit's SSD1306 library, and emails are sent using the SMTP protocol. The IP address is monitored, stored, and compared against the last known IP to trigger an email alert if a change is detected.  

**Hardware:**   
    *Adafruit PiOLED - 128x32 Monochrome OLED    
    *I2C connections (SCL, SDA)  

**Software:**  
Virtual environment for package management:       
    *adafruit-circuitpython-ssd1306  
    *Pillow  
    *smtplib  
    *subprocess

**Setup Instructions:**  

**1. Create Necessary Directories and Files**   
```
mkdir ~/rpi_ip
cd ~/rpi_ip
touch last_ip.txt credentials.txt
```
last_ip.txt: Stores the last known IP address to detect changes.  
credentials.txt: Stores your email credentials in the following format:  
```
from_address=your_email@gmail.com
to_address=recipient_email@gmail.com
subject=IP Address Changed
username=your_email@gmail.com
password=your_password
```
**2. Set Up Virtual Environment**
To avoid conflicts and manage dependencies, create and activate a virtual environment under rpi_pi directory:  
```
mkdir virtual_env
cd virtual_env
python3 -m venv .venv
source .venv/bin/activate
```
**3. Install Dependencies**  
 Inside the virtual environment, install the required packages:
 ```
pip install adafruit-circuitpython-ssd1306
pip install Pillow
```
**4. Download the script from the  github Repo**
Place the folder in the ```~/rpi_ip``` directory.  
Ensure the file paths for credentials.txt and last_ip.txt are correct in the script.  
```
git clone https://github.com/donaldsonlab/pi_IP_screen
```
**5. Test the Script**  
Make sure everything is set up correctly by running the script manually:  
```
cd ~/rpi_ip
source virtual_env/.venv/bin/activate
python3 pi_IP_screen/display_ip_and_email
```
Verify that the IP address displays on the OLED screen and an email is sent if the IP changes.  

**6. Automate the Script on Boot**
 To ensure the script runs on every boot, create a shell script that activates the virtual environment and runs the main Python script:  
 1. Create run_ip_display.sh:
 ```
 cd ~/rpi_ip
nano run_ip_display.sh
```
Add the following content: 
```
#!/bin/bash
source virtual_env/.venv/bin/activate
python3 ip_display.py
```  
2. Make the script executable:
```chmod +x run_ip_display.sh```  

3. Edit Crontab to run on boot:
```crontab -e```
Add the following line at the end of the file to run the script at boot:  
```
@reboot /home/pi/rpi_ip/run_ip_display.sh
```

**Conclusion**
This setup will display the internal IP address of your Raspberry Pi on an OLED screen and send an email notification whenever the IP changes. By automating it on boot, the IP is always displayed and notifications are sent without manual intervention.