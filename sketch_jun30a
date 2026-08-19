#include "BluetoothSerial.h"

BluetoothSerial SerialBT;

const int greenLed = 18;
const int yellowLed = 19;

bool partyRunning = false;

void setup() {

  pinMode(greenLed, OUTPUT);
  pinMode(yellowLed, OUTPUT);

  digitalWrite(greenLed, LOW);
  digitalWrite(yellowLed, LOW);

  Serial.begin(115200);

  SerialBT.begin("ESP32_Smart_Light");

  Serial.println("Bluetooth Started");
}


void loop() {
  if (SerialBT.available()) {
    String command = SerialBT.readStringUntil('\n');
    command.trim();
    Serial.println(command);
    handleCommand(command);
  }

  if (partyRunning) {
    digitalWrite(greenLed, HIGH);
    digitalWrite(yellowLed, LOW);
    delay(300);
    digitalWrite(greenLed, LOW);
    digitalWrite(yellowLed, HIGH);
    delay(300);
  }
}


void handleCommand(String command) {
  if (command == "GREEN_ON") {
    digitalWrite(greenLed, HIGH);
  }
  else if (command == "GREEN_OFF") {
    digitalWrite(greenLed, LOW);
  }

  else if (command == "YELLOW_ON") {
    digitalWrite(yellowLed, HIGH);
  }

  else if (command == "YELLOW_OFF") {
    digitalWrite(yellowLed, LOW);
  }

  else if (command == "ALL_ON") {
    allLightsOn();
  }

  else if (command == "ALL_OFF") {
    allLightsOff();
  }

  else if (command == "DAY") {
    partyRunning = false;
    digitalWrite(greenLed, HIGH);
    digitalWrite(yellowLed, LOW);
  }

  else if (command == "NIGHT") {
    partyRunning = false;
    digitalWrite(greenLed, LOW);
    digitalWrite(yellowLed, HIGH);
  }

  else if (command == "PARTY") {
    partyRunning = true;
  }

  else if (command == "STOP") {
    partyRunning = false;
    allLightsOff();
  }
}


void allLightsOn() {
  partyRunning = false;
  digitalWrite(greenLed, HIGH);
  digitalWrite(yellowLed, HIGH);
}


void allLightsOff() {
  partyRunning = false;
  digitalWrite(greenLed, LOW);
  digitalWrite(yellowLed, LOW);
}
