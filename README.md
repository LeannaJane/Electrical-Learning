## Arduino Hardware

The arduino R2 diagram:

<img width="1089" height="779" alt="image" src="https://github.com/user-attachments/assets/777415cd-28af-4a92-8bd0-d82dadb253c0" />

(Arduino, 2019)

The key components of an arduino board:
 
1. The microcontroller - this is the brain of the arduino, and the component that have programs loaded into it. (Tiny computer that can execute only a number of specific things).
2. USB port - used to connect arduino to computer
3. USB to serial chip - the usb to serial is an important compent, as it helps translating the data that comes from .e.g a computer to the on board microcontroller. This is what makes it possible to program the arduino from the computer.
4. Digital Pins -  Pins that use digital logic (0,1 OR low/high), this is commonly used for switches and to turn on/off an led
5. Analogue pins - pins that can read analogue values in a 10 bit resolution (0-1023).
6. 5V/3.3 V pins - these are pins are used to power external components
7. GND - also known as ground, negative or simply -, is used to complete a circuit, where the electrical level is at 0 volts.
8. VIN - stands for voltage in, where you can connect external power supplies.
<img width="609" height="402" alt="image" src="https://github.com/user-attachments/assets/cd1b0411-19fd-4ea3-a33b-12990b727dae" />

(Arduino, 2019)


Making a basic circuit with an arduino:
Arduino circuit built using tinker cad simulation.  

<img width="596" height="398" alt="image" src="https://github.com/user-attachments/assets/3006076c-360c-43d8-b3ae-57bdde2496f7" />

(Tinkercad, 2023)
 
<img width="655" height="873" alt="image" src="https://github.com/user-attachments/assets/5c1b2b4a-30f5-41ab-b743-32d5e76170fd" />


### Task 1: Wiring a Basic LED Circuit

**Component List:**

- 1 x Arduino Mega 2560 (or Arduino Uno R3)
    
- 1 x LED (Red)
    
- 1 x $330\,\Omega$ Resistor
    
- 2 x Male-to-Male Jumper Cables (Yellow and Purple)
    
- 1 x Breadboard
    
- 1 x USB Power Cable

**Circuit Description:**

Power is supplied from **Digital Pin 3** on the Arduino, routed through the **yellow jumper cable** to the breadboard. The current passes through a **$330\,\Omega$ current-limiting resistor**, which connects directly to the **anode (the long, positive leg)** of the LED.

The current flows through the LED and exits via the **cathode (the short, negative leg)**. From there, it travels through the **purple jumper cable** back to the **GND (Ground) pin** on the Arduino, completing the electrical circuit.

Terminology Notes:

| **LED Term** | **Physical Feature**                 | **Connection**                             | **Function**                          |
| ------------ | ------------------------------------ | ------------------------------------------ | ------------------------------------- |
| **Anode**    | Long Leg                             | Connected to the Resistor / Power side     | The positive entry point for current. |
| **Cathode**  | Short Leg (Flat edge on LED housing) | Connected to the Purple Wire / Ground side | The negative exit point for current.  |

<img width="274" height="184" alt="image" src="https://github.com/user-attachments/assets/6ba6f5f1-46ee-42bd-aa7b-fc3ccb06003b" />

(You, 2019)

```
// Define the pin connected to the LED
const int ledPin = 3; 

void setup() {
  // Initialise digital pin 3 as an output.
  pinMode(ledPin, OUTPUT);
}

void loop() {
  digitalWrite(ledPin, HIGH);   // Turn the LED on (send 5V)
  delay(1000);                  // Wait for a second (1000 milliseconds)
  digitalWrite(ledPin, LOW);    // Turn the LED off (send 0V)
  delay(1000);                  // Wait for a second
}
```








https://github.com/user-attachments/assets/b9c6f28a-2bd9-42b3-9402-2a7749909ef7


### Task 2: Wiring an 8-LED Sequential and Alternating Circuit

**Component List:**

- 1 x Arduino Mega 2560
    
- 8 x LEDs (5 x Yellow, 3 x Blue/Green)
    
- 8 x $330\,\Omega$ Current-Limiting Resistors
    
- 8 x Male-to-Male Jumper Cables (Red, connecting Digital Pins to Resistors)
    
- 1 x Shared Ground Return Wire (Blue/Black)
    
- 1 x Breadboard
    
- 1 x USB Power Cable


**Circuit Description:**

Power is dynamically supplied from a bank of eight consecutive digital pins (**Digital Pins 0 through 7**) on the Arduino Mega. Each pin is connected via an individual red jumper cable to a corresponding row on the breadboard. For every unique row, the current passes through an independent $330\,\Omega$ resistor, which protects the components by limiting current before entering the **anode (long leg)** of each respective LED.

The current exits each LED through its **cathode (short leg)**, dropping into the breadboard’s shared ground rail. A single ground return wire bridges this rail back to the **GND (Ground)** pin on the Arduino, completing the multi-channel electrical circuit.

```
int numOfPins = 8;

void setup() {
  for (int i = 0; i < 8; i++) {
    pinMode(i, OUTPUT);
  }
}

void loop() {
  animStep();
  animOddEven();
  animReset();
}

void animOddEven() {
  for (int i = 0; i < 4; i++) {
    if (i % 2) {
      digitalWrite(0, HIGH);
      digitalWrite(2, HIGH);
      digitalWrite(4, HIGH);
      digitalWrite(6, HIGH);

      digitalWrite(1, LOW);
      digitalWrite(3, LOW);
      digitalWrite(5, LOW);
      digitalWrite(7, LOW);
    } else {
      digitalWrite(0, LOW);
      digitalWrite(2, LOW);
      digitalWrite(4, LOW);
      digitalWrite(6, LOW);

      digitalWrite(1, HIGH);
      digitalWrite(3, HIGH);
      digitalWrite(5, HIGH);
      digitalWrite(7, HIGH);
    }
    delay(300);
  }
}

void animStep() {
  for (int i = 0; i < 8; i++) {
    digitalWrite(i, HIGH);
    delay(150);
    digitalWrite(i, LOW);
  }
}

void animReset() {
  for (int i = 0; i < 8; i++) {
    digitalWrite(i, LOW);
  }
}
```

References:
Arduino (2019). _Arduino Forum - Index_. [online] Arduino.cc. Available at: https://forum.arduino.cc/.

‌You, W. (2019). _LED Technology | What You Need to Know_. [online] commercialledlights.com. Available at: https://share.google/X7dUGLJnF4wI6lz4a [Accessed 17 May 2026].

‌Tinkercad (2023). _Tinkercad | From mind to design in minutes_. [online] www.tinkercad.com. Available at: https://www.tinkercad.com/dashboard.
