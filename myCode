/*-------defining Inputs------*/
#define LS A0      // left sensor
#define RS A1     // right sensor
#define TS A2    // trash sensor
#define inPin 2    // push button

/*-------defining Outputs------*/
#define LM1 3   // left motor terminal 1 and 2
#define LM2 4           
#define RM1 5       // right motor terminal 1 and 2
#define RM2 6
#define TM1 7   // trash lid motor terminal 1 and 2
#define TM2 8           
#define BZ  12    // buzzer

/*------LIBRARY DEFINE------*/
#include<SoftwareSerial.h>

/*------GLOBAL VARIABLES DEFINE------*/
SoftwareSerial mySerial(0,1);
int LeftIR=0;
int RightIR=0;
int TrashIR=0;
int val = 0;

/*------SMS FUNCTION------*/
void SendMessage()
{
  mySerial.println("AT+CMGF=1"); //Sets in Text module
  delay(1000);
  mySerial.println("AT+CMGS=\"+919600264511\"\r");
  delay(1000);
  mySerial.println("Trash can is FULL, please Empty it");
  delay(1000);
  mySerial.println((char)26); //ASCII code of CTRL+Z
  delay(1000);
}

/*------SETUP FUNCTION------*/
void setup()
{
  mySerial.begin(19200);
  Serial.begin(19200);
  Serial.begin(9600);
  delay(100);
  pinMode(LS, INPUT);
  pinMode(RS, INPUT);
  pinMode(TS, INPUT);
  pinMode(inPin, INPUT);
  pinMode(LM1, OUTPUT);
  pinMode(LM2, OUTPUT);
  pinMode(RM1, OUTPUT);
  pinMode(RM2, OUTPUT);
  pinMode(TM1, OUTPUT);
  pinMode(TM2, OUTPUT);
  pinMode(BZ, OUTPUT); 
}

/*------LOOP FUNCTION------*/
void loop()
{
  LeftIR = analogRead(LS);
  RightIR = analogRead(RS);
  TrashIR = analogRead(TS);
  val = digitalRead(inPin);  // read input value
  delay(1000);
  if(val == LOW)    // button pressed 
  {
    Serial.println("Button pressed, Keep pressing...");
    if(analogRead(TS) == HIGH)  //Sensor of Trash can, checks if there's any trash, 
    {                         //If YES detects and goes HIGH, and on HIGH following code should execute 
	  Serial.println("Trash sensor");
	  Serial.println(TS);
	  delay(2000);
	  Serial.println("Lid motor in clockwise direction");
	  digitalWrite(TM1, LOW);   // Trash can lid rotates in clockwise thus closing the lid
	  digitalWrite(TM2, HIGH);
	  delay(2000);
	  tone(12,200,3500);        //Stops
	  Serial.println("Lid motor deactivates");
	  digitalWrite(TM1, LOW);   // Trash motor disengages
	  digitalWrite(TM2, LOW);
	  delay(500); 
	  Serial.println("Left motor deactivates");
	  digitalWrite(LM1, HIGH);
	  digitalWrite(LM2, HIGH);
	  delay(1000);
	  Serial.println("Right motor deactivates");
	  digitalWrite(RM1, HIGH);
	  digitalWrite(RM2, HIGH);
	  Serial.println("Sending an SMS to Worker");
	  if(Serial.available()>0)
	  {
	      SendMessage();
	  }
	  if(mySerial.available()>0)
	  {
	      Serial.write(mySerial.read());
	  }
     }
  else{                  // If not HIGH, executes Line Following code 
  if(LeftIR > RightIR)       // Turn left
  {
    Serial.println("Left sensor value is HIGH, Turn Right");
    Serial.println(LS);
    Serial.println("Lid motor runs in Anti-clockwise direction");
    digitalWrite(TM1, HIGH);  // Trash can lid rotates in anticlockwise direction
    digitalWrite(TM2, LOW); 
    delay(2000);
    Serial.println("Lid motor deactivating...");
    digitalWrite(TM1, LOW);   // Trash motor disengages
    digitalWrite(TM2, LOW);
    Serial.println("Lid motor deactivates");
    delay(500); 
    Serial.println("Left motor deactivating...");
    digitalWrite(LM1, LOW);
    digitalWrite(LM2, LOW);
    Serial.println("Left motor deactivates");
    delay(1000);
    Serial.println("Right motor runs");
    digitalWrite(RM1, LOW);
    digitalWrite(RM2, HIGH);
  }
    
  if(LeftIR < RightIR)       // Turn right
  {
    Serial.println("Right sensor value is HIGH, Turn Left");
    Serial.println(RS);
    Serial.println("Lid motor runs in Anti-clockwise direction");
    digitalWrite(TM1, HIGH);  // Trash can lid rotates in anticlockwise direction
    digitalWrite(TM2, LOW); 
    delay(2000);
    Serial.println("Lid motor deactivating...");
    digitalWrite(TM1, LOW);   // Trash motor disengages
    digitalWrite(TM2, LOW);
    Serial.println("Lid motor deactivates");
    delay(500);
    Serial.println("Right motor deactivating...");
    digitalWrite(RM1, LOW);
    digitalWrite(RM2, LOW);
    Serial.println("Right motor deactivates");
    delay(1000);
    Serial.println("Left motor runs");
    digitalWrite(LM1, LOW);
    digitalWrite(LM2, HIGH);
  }
    
  if(LeftIR == RightIR)      // stop
  {
    Serial.println(LS);
    Serial.println("Sensor values are equal, STOP");
    Serial.println("Lid motor runs in clockwise direction");
    digitalWrite(TM1, LOW);   // Trash can lid rotates in clockwise direction
    digitalWrite(TM2, HIGH);
    delay(2000);
    tone(12,200,3500);        //Stops
    Serial.println("Lid motor deactivating...");
    digitalWrite(TM1, LOW);   // Trash motor disengages
    digitalWrite(TM2, LOW);
    Serial.println("Lid motor deactivates");
    delay(500);   
    Serial.println("Right motor deactivating...");
    digitalWrite(RM1, HIGH);
    digitalWrite(RM2, HIGH);
    Serial.println("Right motor deactivates");
    delay(500); 
    Serial.println("Left motor deactivating...");
    digitalWrite(LM1, HIGH);
    digitalWrite(LM2, HIGH);
    Serial.println("Left motor deactivates");
    delay(1000);
    tone(12,100,3000);
    delay(1000);    
  }
 }
 }
else{             // button released
 }
}
