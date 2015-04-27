# Digispark_DigiUSB-SoftSerial

This is a modified DigiUSB (V-USB) library that provides digispark to use DigiMouse/DigiKeyboard/DigiJoystick with SoftSerial (SoftwareSerial) library at same time. It allows, for example, using a Bluetooth module to control the mouse or keyboard.

-------------------------------------------------------------------------------------------------------------------------

How to install:
  - Copy the digistump folder inside .../Arduino-X.X.X/hardware (Overwrite the folder if it exists).

How to use:
  - Connect P2 pin to P3 pin (otherwise you will get: "USB device not recognized").
  - Use the P0 for RX pin and P1 for TX pin of the Software serial library (PWM pins).

-------------------------------------------------------------------------------------------------------------------------

Example:

```
#include <TinyPinChange.h>
#include <SoftSerial.h>
#include <DigiMouse.h>

#define P_RX 0
#define P_TX 1

char a, s, d;
int x, y, c;

SoftSerial BLE(P_RX, P_TX);

void setup()
{
    BLE.begin(9600);
    DigiMouse.begin();
}

void loop()
{
    if(BLE.available() >= 3)
    {
        a = BLE.read();
        s = BLE.read();
        d = BLE.read();
        
        mouse_action(a, s, d); // Determine x, y and c for move the mouse
    }
    DigiMouse.move(x, y, c);
    DigiMouse.update();
}
```

-------------------------------------------------------------------------------------------------------------------------
