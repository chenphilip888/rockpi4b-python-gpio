Python gpio experiments on the ROCK PI 4B board.

The following 8 tests are included: ( see below for tests summary )
1. uart test
2. led test
3. button test
4. pwm led test
5. i2c lcd test
6. tongsong
7. servo
8. spi oled test

-------------------------------------------------------------------
To compile and flash to sd card:
cd rockpi4b-python-gpio
Download OS:
wget https://dl.radxa.com/rockpi/images/debian/rockpi4-debian-stretch-desktop-arm64-20190730_2022-gpt.img.gz
gunzip rockpi4-debian-stretch-desktop-arm64-20190730_2022-gpt.img.gz
Use balenaEtcher to burn img to sd card.
eject sd card.
Plugin sd card to PC.
generate pwm.dtbo:
dtc -O dtb -o pwm.dtbo -b 0 -@ pwm.dts
sudo mkdir /media/$USER/tmp
sudo mount -t vfat /dev/mmcblk0p4 /media/$USER/tmp
sudo cp hw_intfc.conf /media/$USER/tmp
sudo cp pwm.dtbo /media/$USER/tmp/overlays
sync
sudo umount /media/$USER/tmp
eject sd card.
Plugin the sd card to ROCK PI 4B board
Connect ROCK PI 4B gpio Pin 8 to serial USB cable TX.
Connect ROCK PI 4B gpio pin 10 to serial USB cable RX. 
Connect ROCK PI 4B gpio pin 39 to serial USB cable ground. 
Type "script ~/outputfile.txt" on PC.
Plugin serial USB cable to PC.
Type "sudo screen /dev/ttyUSB0 1500000" on PC.
Power on ROCK PI 4B board
sudo dpkg-reconfigure tzdata  US/Pacific-New
setup wifi:
nmcli dev wifi list
sudo nmcli con add con-name WiFi ifname wlan0 type wifi ssid mywifissid
sudo nmcli con modify WiFi wifi-sec.key-mgmt wpa-psk
sudo nmcli con modify WiFi wifi-sec.psk mypassword
sudo nmcli con up WiFi
sudo ifconfig
date
ssh linaro@192.168.86.123  ( The original password is "linaro" )
passwd
vi nosleep.sh ( add following line to disable sleep feature )
sudo systemctl mask sleep.target suspend.target hibernate.target hybrid-sleep.target
./nosleep.sh
sudo dmesg -n 1
sudo vi /etc/rc.local ( add sudo dmesg -n 1 )
sudo shutdown -h now
Power off ROCK PI 4B board
Power on ROCK PI 4B board
ssh linaro@192.168.86.123
wget -O - apt.radxa.com/stretch/public.key | sudo apt-key add -
sudo apt-get update
sudo apt-get upgrade
sync
sudo shutdown -h now
Power off ROCK PI 4B board
Power on ROCK PI 4B board
ssh linaro@192.168.86.123
sudo apt-get install python-dev python-pip python-setuptools python3-dev python3-pip python3-setuptools dnsutils apache2 vsftpd ftp build-essential git libssl-dev nmap net-tools libssl-dev dkms libncurses5-dev libncursesw5-dev
sudo cat /proc/device-tree/spi@ff1e0000/status
sudo cat /proc/device-tree/pwm@ff420010/status
sudo cat /proc/device-tree/i2c@ff160000/status
if result is disabled, need to copy hw_intfc.conf and pwm.dtbo to sd card as above and reboot.
ls -l /sys/class/pwm

-------------------------------------------------------------------------
Install python library:
sudo pip install serial
sudo pip install pyserial
sudo pip install spidev
sudo apt-get install python-smbus
git clone https://github.com/doceme/py-spidev.git
cd ~/py-spidev
sudo python setup.py install
sudo python3 setup.py install

cd ~/rockpi4b-python-gpio
sudo ./gpio_test.py
When done all tests, hit 'q' to exit tests.
sudo shutdown -h now
Power off the ROCK PI 4B board.
Unplug serial USB cable from PC.
Type "exit" on PC.

-------------------------------------------------------------------------
Here are the summary of the tests: ( see https://wiki.radxa.com/Rockpi4/hardware/gpio )
These tests used Seeed Grove  starter kit LED, button, buzzer, Grove-LCD RGB Backlight V3.0 JHD1313M2, Analog Servo and Adafruit SSD1306 128x32 SPI OLED Display.
1. uart test.
   This test will send uart4 tx to uart4 rx for loopback.
   It sends 0 to 255 to uart4 tx and receive 0 to 255 from uart4 rx.
   Connect gpio pin 19 to pin 21.
2. led test.
   This test will blink led 5 times. 
   Connect gpio pin 16 to led control. 
   Connect gpio pin 2 to led 5V. 
   Connect gpio pin 9 to led ground.
3. button test. 
   Connect gpio pin 16 to led control. 
   Connect gpio pin 2 to led 5V. 
   Connect gpio pin 9 to led ground. 
   Connect gpio pin 18 to button control.
   Connect gpio pin 4 to button 5V.
   Connect gpio pin 6 to button ground.
4. pwm led test.
   This test will dim led 10 times.
   Connect gpio pin 13 to led control.
   Connect gpio pin 2 to led 5V.
   Connect gpio pin 9 to led ground.
5. i2c lcd test.
   This test will change lcd backlight color for 5 cycles.
   Then it will display two sentences on lcd display.
   Connect gpio pin 3 to lcd display SDA.
   Connect gpio pin 5 to lcd display SCL.
   Connect gpio pin 2 to lcd display 5V.
   Connect gpio pin 9 to lcd display ground.
6. tongsong.
   This test will generate song using buzzer.
   Connect gpio pin 13 to buzzer control.
   Connect gpio pin 2 to buzzer 5V.
   Connect gpio pin 9 to buzzer ground. 
7. servo.
   This test will turn servo 90 degree - 180 degree - 90 degree - 0 degree etc.
   Connect gpio pin 13 to servo control.
   Connect gpio pin 2 to servo 5V.
   Connect gpio pin 9 to servo ground.
8. spi oled test.
   This test will show some ascii characters on the oled display.
   Connect gpio pin 16 to oled display DC.
   Connect gpio pin 33 to oled display CS.
   Connect gpio pin 29 to oled display TX.
   Connect gpio pin 7 to oled display CLK.
   Connect gpio pin 1 to oled display 3.3V.
   Connect gpio pin 9 to oled display ground.

-----------------------------------------------------------------------------
