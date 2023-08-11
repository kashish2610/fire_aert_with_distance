# fire_aert_with_distance
int btnpin=7;
const int flameSens = A0;//set flame sensor to pin A0 
const int speaker = 8;//set speaker to pin 8
int flameVal;//set up the data variable for the sensor
 int i=0;
int  statespeaker=LOW;
int  counter=0;
int buttonState = 0;         // variable for reading the pushbutton status
int count_value =0;
int prestate =0;
const int ledPin =    11;   
volatile int state = LOW;
void setup() {

  
Serial.begin(9600);//begin the serial monitor
pinMode(speaker, OUTPUT);//define the speaker as an output
pinMode(flameSens, INPUT);//define flame sensor as an input

}

void loop() {

int flameVal = analogRead(flameSens);//read the sensor value of flame sensor

if (flameVal < 1000){//if the data us less than 1023 then set off an alarm
  
  digitalWrite(speaker,HIGH);
  Serial.println("FLAME");
}
 buttonState = digitalRead(btnpin);

  // check if the pushbutton is pressed. If it is, then the buttonState is HIGH:
  if (buttonState == HIGH && prestate == 0) {
    count_value++;
    Serial.println(count_value);
    // turn LED on
    digitalWrite(ledPin, HIGH);
    digitalWrite(speaker,HIGH);
  Serial.println("FLAME");
    delay(1000);
    // turn LED off
    digitalWrite(ledPin, LOW);
 
    prestate = 1;
  } else if(buttonState == LOW) {
    prestate = 0;
  }
  

 else{
  digitalWrite(speaker, LOW);// if else don't set off alarm
  Serial.println("COOL");
 }

       Serial.println(count_value);
Serial.println(i);
Serial.println(flameVal);
//print the data to the serial monitor
delay(1000);
}
