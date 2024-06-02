// add Your credentials 
#define BLYNK_TEMPLATE_ID "Templet token" 
#define BLYNK_TEMPLATE_NAME "Project Name"
#define BLYNK_AUTH_TOKEN "Auth Token"
#define BLYNK_PRINT Serial

#include <BlynkSimpleEsp32.h>
#include "WiFi.h" 


char auth[] = BLYNK_AUTH_TOKEN; // the auth code for Blynk App
char ssid[] = ""; // username or ssid of Wi-Fi
char pass[] = ""; // password of Wi-Fi

// Object of Timer Class
BlynkTimer timer;

// sensor variables
int smokeSensor = 5;
int data = 0;
int fireSystem = 12;

// button pin 
#define bulb_btn 19
#define fan_btn 21

// relays pin
#define bulb_relay 25
#define fan_relay 26

// state variables 
int bulb_relay_state = 0;
int fan_relay_state = 0;

// Virtual pins 
#define bulb_vpin    V0
#define fan_vpin    V1
#define smokeGuage_vpin V4

// This function is called every time the device is connected to the Blynk.Cloud
// Request the latest state from the server
BLYNK_CONNECTED() {
  Blynk.syncVirtual(bulb_vpin);
  Blynk.syncVirtual(fan_vpin);
  Blynk.syncVirtual(smokeGuage_vpin);
}

// This function is called every time the Virtual Pin state change
//i.e when web push switch from Blynk App or Web Dashboard
BLYNK_WRITE(bulb_vpin) {
  bulb_relay_state = param.asInt();
  digitalWrite(bulb_relay, bulb_relay_state);
}

BLYNK_WRITE(fan_vpin) {
  fan_relay_state = param.asInt();
  digitalWrite(fan_relay, fan_relay_state);
}
////////////// SET UP Function ////////////// 
void setup() {
  Blynk.begin(auth, ssid, pass);
  // Debug console
  Serial.begin(115200);

  // Btn PIN CONFIG
  pinMode(bulb_btn, INPUT_PULLUP);
  pinMode(fan_btn, INPUT_PULLUP);
  
  // RELAYS PIN CONFIG
  pinMode(bulb_relay,OUTPUT);
  pinMode(fan_relay, OUTPUT);

  // FIRE SYSTEM PIN CONFIG
  pinMode(fireSystem,OUTPUT); 
  pinMode(smokeSensor, INPUT);

  //During Starting all Relays should TURN OFF
  digitalWrite(bulb_relay, HIGH);
  digitalWrite(fan_relay, HIGH);

  timer.setInterval(2500L, sendSensor); // blyn timer for calling Smoke sensor function.
}

////////////// LOOP Function ////////////// 
void loop(){
  Blynk.run();
  timer.run();

  listen_push_buttons();  
}


// button controller
void listen_push_buttons(){

    if(digitalRead(bulb_btn) == LOW){
      delay(200);
      control_relay(1);
      Blynk.virtualWrite(bulb_vpin, bulb_relay_state); //update button state
    }
    else if (digitalRead(fan_btn) == LOW){
      delay(200);
      control_relay(2);
      Blynk.virtualWrite(fan_vpin, fan_relay_state); //update button state
    }
}

// relay controller
void control_relay(int relay){

  if(relay == 1){
    bulb_relay_state = !bulb_relay_state;
    digitalWrite(bulb_relay, bulb_relay_state);
    delay(50);
  }
  else if(relay == 2){
    fan_relay_state = !fan_relay_state;
    digitalWrite(fan_relay, fan_relay_state);
    delay(50);
  }
}


// smoke sensor 
void sendSensor(){
 
  int data = digitalRead(smokeSensor);
  Blynk.virtualWrite(smokeGuage_vpin, data);
  Serial.print("Pin A0: ");
  Serial.println(data);

  if(!data){
    digitalWrite(fireSystem, LOW);
    Blynk.logEvent("gas_sensor","Gas Leakage Detected");
  }
  else {
    digitalWrite(fireSystem, HIGH);
  }
}
