# SMART-SECURITY-CAMERA
3.4.1 Raspberry Pi Model B+
This is the model that was chosen to implement the project. It has merits over other models in that it has increased number of USB ports and large number of GPIO pins. Moreover, this piece of hardware was available at the department.(refer to section two for diagram)
3.3.2	Booting Up the Pi Model Raspbian

‘Wheezy’ image was written into the 4GB Micro SD card. This was the operating system chosen to run on the Pi because the OS has been optimized and ported to the Raspberry Pi ARM architecture. This OS has very good integration with the hardware and comes preloaded with a GUI and development tools. After slotting in the Micro SD card and connecting RJ45 Ethernet cable to the Pi and the personal computer with Putty software (Putty is an SSH client used to remotely access and control the Pi from computer running on Windows platform) the system was powered. Putty was then started and the default static IP address of the Pi was typed into the host name field. While doing this, windows pc was set to manual IP configuration. This was to allow it communicate with the Raspberry Pi.
3.3.3	Setting Up internet connection on the Pi
Internet was necessary in so that the Pi can communicate over network protocols and thus allow for installation of necessary Python packages. The architecture below was used to achieve that. 


Since the broadcast router uses Dynamic Host Configuration Protocol (DHCP) to dish out IP addresses to devices connected to it, it was necessary to change the IP address of the Pi from static to dynamic. This was done by editing the network interfaces file using the command;
sudo nano /etc/network/interfaces
3.3.4	Enabling the Pi Camera
This is the camera made specifically for the Raspberry Pi. It was hooked to the raspberry pi through CSI-2 electrical port which is an extremely fast port. To configure and enable the camera, the following commands were executed at the CLI of the raspberry pi:
sudo apt_get update sudo apt_get upgrade sudo raspi-config
After these configuration settings, the system was rebooted. This was done to ensure that the camera was allocated enough space in memory. The camera takes 5MP image and has a resolution of 1080 by 890. And to ensure that the camera was well configured and functional, the following command was executed.
sudo ras pistill –o image.png
This by default this command takes a three second image and save it in a file called image.png.
3.3.5	Setting Up the Passive Infrared Sensor
This is formed the prime motion sensor. It was used to control the entire system. The device used here was HC501SR passive infrared sensor. The detection range is 7 meters by 140(degrees) coning angles. It has a delay time of 16 seconds but adjustable. The ambient temperature is 253K-323K. It was powered directly from the Pi through the 5V dc supply pin. Its output was connected as the input to the programmable GPIO pin.
3.3.6	Automatic Light Simulation
An LED was used to simulate an automatic light control. This was designed to be controlled through the action of a PIR sensor. This device was connected to the GPIO pin through a
220Ω resistor.
 3.4.7 Hardware Architecture
The entire system modules were interfaced together as shown below. 
3.5	Design Software
3.5.1	The flowchart of the Raspberry Pi Based Security system

This following flowchart was used to design and thus document the security systems project. It illustrates the series of events starting from intrusion event up to the point when it sends out an alert. This algorithm was implemented using a Python script below presents the basic flowchart of the entire system.

3.5.2	System initialization and configuration
This involved the following tasks:
Importing Python libraries and packages. These libraries are predefined and help in making the interfaced modules work properly.
Pi Camera setting and configuration.
GPIO settings and pin initialization: (the channel was set using the BCM channel numbering. Passive infrared pin channel was set to read mode while the led channel was set to drive/write mode
a)	Read a Channel
In order to read the value of any GPIO pin, simply type; GPIO.input(channel)
b)	Drive a channel

24
 
In order to drive a channel of GPIO pin, type; GPIO.output(channel, status) This sequence of events can be elaborated well using the block diagram below.



3.5.3	Generating and sending e-mail
After configuring the system to send an alert to the predefined subscriber, it was then necessary to generate and send the mail. Multipurpose Internet Mail Extension (MIME) package was then called and used to generate the attachment. MIME supports characters other than ASCII, non – text attachments (audio, video and application programs) etc. It thus extends the format of an email. Simple Mail Transfer Protocol (SMTP) program was then used to deliver the email from the Raspberry Pi to the configured mailhub. This can be summarized using the blocks below.

