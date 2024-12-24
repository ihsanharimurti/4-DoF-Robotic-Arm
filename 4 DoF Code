#include <ESP32Servo.h>

// Define pins for joysticks and potentiometer
#define VERT_PIN0 35
#define HORZ_PIN0 34
#define VERT_PIN1 33
#define HORZ_PIN1 39
#define POT_PIN 32



// Define pins for servos
const int servoPins[] = {4, 2, 15, 13, 12};
Servo servos[5]; // Array to hold servo objects

// Function to read analog input and map its value to a specific range
int readAndMap(int pin, int inMin, int inMax, int outMin, int outMax) {
  int value = analogRead(pin);
  return map(value, inMin, inMax, outMin, outMax);
}

void setup() {
  Serial.begin(9600);

  // Initialize all servos at 90 degrees
  for (int i = 0; i < 5; i++) {
    servos[i].attach(servoPins[i]);
    servos[i].write(90);
  }
}

void loop() {
  // Read values from joysticks and potentiometer
  int vert0 = readAndMap(VERT_PIN0, 0, 4095, -100, 100);
  int horz0 = readAndMap(HORZ_PIN0, 0, 4095, -100, 100);
  int vert1 = readAndMap(VERT_PIN1, 0, 4095, -100, 100);
  int horz1 = readAndMap(HORZ_PIN1, 0, 4095, -100, 100);
  int pot = readAndMap(POT_PIN, 0, 4095, 0, 180);


  if (vert0 < -2 && vert0 > -6){
      vert0 = 0;
  } 
  if (horz0 < -6 && horz0 > -10){
      horz0 = 0;
  } 
  if (vert1 < -6 && vert1 > -10){
      vert1 = 0;
  } 
  if (horz1 < -1 && horz1 > -5) {
      horz1 = 0;
  }



  // Print the values to the Serial Monitor
  Serial.printf(
      "Vertical0: %3d\tHorizontal0: %3d\tVertical1: %3d\tHorizontal1: %3d\tPotentiometer: %4d\n", 
      vert0, horz0, vert1, horz1, pot
  );

  // Calculate servo angles based on the input values
  int angles[] = {
    map(pot, 180, 0, 0, 180),      // Servo 0 - Potentiometer
    map(vert0, -100, 100, 0, 180), // Servo 1 - Vertical Joystick 0
    map(vert1, -100, 100, 0, 180), // Servo 2 - Vertical Joystick 1
    map(horz0, -100, 100, 0, 180), // Servo 3 - Horizontal Joystick 0
    map(horz1, -100, 100, 0, 180)  // Servo 4 - Horizontal Joystick 1
  };

  // Move the servos to the calculated angles
  for (int i = 0; i < 5; i++) {
    servos[i].write(angles[i]);
  }

  // Add a small delay for stability
  delay(15);
}
