(1)Project Introduction
This project aims to design and develop an integrated IoT system to effectively monitor and control environmental parameters, through the combined use of hardware, software and cloud-based solutions. This project aims to create an efficient and user-friendly environmental monitoring solution using STM32 microcontroller-based hardware, WeChat mini program for user interaction and a cloud-based panel for data storage and processing. 

(2)Hardware list
STM32F103C8T6      Microcontroller  5V
MQ-2               Smoke Module  5V
MQ-7               Carbon Monoxide Module  5V
MQ-135             Air Quality Module  5V
DHT11              Temperature and humidity Module  5V  
BMP280             Atmospheric pressure intensity and Altitude module  5V
BH1750             Light intensity Module  5V
MQ-6               Combustible gas module  5V
GP2Y1014AU         PM2.5 sensor  5V
ESP8266-01S        WiFi Module  3.3V
0.96 inch          Oled screen  5V
1.8 inch           TFT screen  5V
                   Led light  5V
                   Individual buttons  5V
Keil5
Mini Program Development Tools
MQTT.fx
Node.js
MySQL
Navicat Premium 15


(3)Hardware function
The device includes the detection module, the display and the LEDs and control buttons used to simulate the electrical appliances. When the device is started, the microcontroller initialises all the modules and the initialised state is displayed on the oled screen. After the initialisation is complete, the device connects to the WiFi and the server. After a successful connection, the detection modules start working. All detection data will be transferred to the TFT screen and the WiFi module via the microcontroller. The detection data will be uploaded to the cloud via the WiFi module. The real time data of all the detection modules can be seen on the TFT screen. The four LEDs in the device represent the air conditioning heating mode, the air conditioning cooling mode, the humidifier and the alarm system and there are four buttons to control the LEDs. Because the program in this project almost fills up the memory of the microcontroller, there are sometimes short delays. 

The alarm system has an anti-touch function: for example when the light intensity is too high，the alarm will be turned on automatically . If the light intensity is still high after the alarm has been manually switched off, the alarm will be activated again after a certain period of time. If the alarm is switched on manually, but the value is normal, the alarm will be switched off automatically after a period of time.

(4)Server
In this project, the server used was purchased from Tencent Cloud, and MQTT and EMQX were built onto the server and used as publishers to transfer data. The IP address of the server is: 110.40.167.13, and the IP address of the EMQX platform is: http://110.40.167.13:18083. The mini-program and the cloud dashboard both use port 8084/8083.

(5)Software 
Because publishing the applet required several reviews, the simulation was performed in the applet developer tool and the applet was used as a subscriber to fetch data from MQTT. The applet includes a login page, a live data page, a control page and a user page. On the login page, users can log in after signing up for an account and bind their mobile phone number to change their password. On the real-time data page, you can see the real-time detection data as well as the current location and weather. On the control page, the status of the LED lights in the device is updated to the software in real-time, and can be controlled by switching on and off the LED lights in the device. Because of server delays and limitations when the applet is not published, there are sometimes short delays or failures when controlling the device. On the user page, you can view the time of each login.

(6)Cloud Dashboard
The cloud dashboard is built and developed on node-red, with nodes for node-red, MQTT, email and MySQL. Node-red takes the data from MQTT and transfers it to the Dashboard and MySQL databases, and adds the corresponding time to each data stored in the database. When the alarm system is switched on, it sends an email to the user. The cloud dashboard includes a real-time data and control page, a short-term data trend page and a database page. The real-time data and control page is used for the same functions as the mini-program, updating data and controlling devices in real-time. In the short-term data trend page, the trend of each data can be observed by a line graph. In this project the status of the LED and alarm system is represented by 1 and 0 for on and off. In the database page, the user can select the date, and node-red will get all the data for the corresponding time according to the date selected.







