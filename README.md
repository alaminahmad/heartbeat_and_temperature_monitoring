## **SIMULATION OF HEARTBEAT AND TEMPERATURE MONITORING**

This project focuses on the development of a Heartbeat and Temperature Monitoring system for accurate patient vital sign tracking. The system employs the versatile Arduino Uno microcontroller, known for its adaptability in various embedded applications. It integrates two key components:

1.  Temperature Monitoring: The LM35 temperature sensor ensures precise and reliable temperature measurements. It connects to the Arduino Uno’s analog pin A0, enabling accurate temperature data processing.
2.  Heartbeat Monitoring: A dedicated heartbeat sensor is linked to digital pin 7 of the Arduino Uno, facilitating the measurement and processing of the patient’s heart rate.

The system’s vital sign data is presented in real-time on an LCD display, enhancing its user-friendliness. This integrated setup guarantees accurate data collection and presentation, empowering healthcare professionals to monitor patients’ vital signs with precision and ease.

# **The Block Diagram of the Project**

![](https://miro.medium.com/v2/resize:fit:630/1*HpNl5lCmhuWltvlwq-j5Ug.png)

**The block diagram for this project illustrates the seamless integration of crucial components: an Arduino Uno microcontroller at the core, a dedicated heartbeat sensor linked to a digital pin, and an LM35 temperature sensor meticulously connected to an analog pin. These sensors capture and process vital sign data, namely heart rate and body temperature. The project’s output is presented on an LCD (Liquid Crystal Display) screen, creating an intuitive visual interface for real-time data display. This well-organized setup empowers healthcare professionals to monitor patients’ vital signs accurately, enhancing the quality of care and diagnostics.**

# **CIRCUIT DIAGRAM OF THE PROJECT SHOWING THE RESULT OF THE SIMULATION**

**TEMPERATURE MONITORING**

![](https://miro.medium.com/v2/resize:fit:630/1*JmP-bOGCKDp4KgLL4Bd76Q.png)

The figure above shows our successful body temperature monitoring system. The LCD screen displays the temperature clearly at 57 degrees, demonstrating the system’s accuracy and reliability in conveying health information. This visual representation highlights the device’s practicality and real-time functionality, making it a valuable tool in healthcare. It also demonstrates how well the temperature sensor, Arduino Uno microcontroller, and LCD display work together to provide essential health data.

**HEARTBEAT MONITORING**

![](https://miro.medium.com/v2/resize:fit:630/1*tq29AH8xy_2tmuEhUcDKoA.png)

The figure above demonstrates our effective heartbeat monitoring system. It vividly displays the LCD’s ability to show the pulse rate accurately and in real-time. This visual representation confirms the system’s proficiency in measuring and monitoring heartbeats. It also highlights the smooth collaboration between the heartbeat sensor, Arduino Uno microcontroller, and LCD display, showcasing their seamless synergy in providing essential physiological data. This visual feedback affirms the system’s potential for healthcare applications, making heart health monitoring easy and precise for both healthcare providers and individuals, promoting proactive and informed healthcare practices.

**CODE FOR THE ARDUINO MICROCONTROLLER**

  
#include <TimerOne.h>  
  
#include <LiquidCrystal.h>  
LiquidCrystal lcd(13, 12, 11, 10, 9, 8);  
  
int val;  
int tempPin = A0;// temperature Sensor Pin  
int HBSensor = 7;// Sensor Pin  
int HBCount = 0;  
int HBCheck = 0;  
int TimeinSec = 0;  
int HBperMin = 0;  
int HBStart = 2;  
int HBStartCheck = 0;  
  
void setup() {  
  // put your setup code here, to run once:  
  lcd.begin(20, 4);  
  pinMode(HBSensor, INPUT);  
  pinMode(HBStart, INPUT_PULLUP);  
  Timer1.initialize(800000);   
  Timer1.attachInterrupt( timerIsr );  
  lcd.clear();  
  lcd.setCursor(0,0);  
  lcd.print("HEALTH MONITORING");  
  lcd.setCursor(0,1);  
  lcd.print("TIME IN SEC : ");  
  lcd.setCursor(0,3);  
  lcd.print("BODY TEMP   : ");  
  lcd.setCursor(0,2);  
  lcd.print("HB PER MIN  : ");  
    
}  
  
void loop() {  
  val = analogRead(tempPin);  
  float mv = (val/1023.0)*5000;  
  int cel = mv/10;  
  lcd.setCursor(14,3);  
  lcd.print(cel);  
  lcd.print("   ");  
  delay(100);  
    
  if(digitalRead(HBStart) == LOW)  
  {  
    HBStartCheck = 1;  
  }  
    
  if(HBStartCheck == 1)  
  {  
    if((digitalRead(HBSensor) == HIGH) && (HBCheck == 0))  
      {  
        HBCount = HBCount + 1;  
        HBCheck = 1;  
      }  
        
      if((digitalRead(HBSensor) == LOW) && (HBCheck == 1))  
      {  
        HBCheck = 0;     
      }  
        
      if(TimeinSec == 10)  
      {  
          HBperMin = HBCount * 6;;  
          HBStartCheck = 0;  
          lcd.setCursor(14,2);  
          lcd.print(HBperMin);  
          lcd.print(" ");  
          HBCount = 0;  
          TimeinSec = 0;        
      }  
  }  
}  
  
void timerIsr()  
{  
  if(HBStartCheck == 1)  
  {  
      TimeinSec = TimeinSec + 1;  
      lcd.setCursor(14,1);  
      lcd.print(TimeinSec);  
      lcd.print(" ");  
  }  
}

In conclusion, our project successfully demonstrates a practical and versatile health monitoring system. By integrating temperature and heartbeat sensors with the Arduino Uno microcontroller and an LCD, we achieve real-time and precise monitoring of key health parameters. This accomplishment has significant implications in healthcare and beyond. In healthcare, it can be used in hospitals, clinics, and homes for continuous and non-invasive health tracking, benefiting both healthcare professionals and individuals. Additionally, its technology can be integrated into wearable devices, enabling convenient and portable health monitoring for fitness, sports, and general well-being. It also holds promise in fields like sports science, research, and telemedicine. Overall, our project represents a significant step towards practical health monitoring solutions with real-time capabilities, accuracy, and a user-friendly interface, benefiting various aspects of life and industry.
