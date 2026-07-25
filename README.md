Smart Medication Dosage Adjustment System (Simulation)
An ESP32-based simulation of a remote-controlled medical infusion dosage
system, built and tested in Wokwi.
⚠️ Educational simulation only. This project is a learning exercise in
IoT + embedded safety logic. It is not a certified medical device and must
never be connected to real infusion hardware or used on patients.
Features
Remote dashboard control — a slider on Adafruit IO (0–100 mg/hr) publishes
the target dose over MQTT.
Local manual override — a potentiometer lets the "bedside" operator take
control; a push button returns control to the dashboard.
Real-time OLED display — shows mode (Manual/Dashboard), target dose,
current (ramped) dose, and safety status.
Three-tier safety indication
🟢 Normal: ≤ 60 mg/hr
🟡 Warning: 61–80 mg/hr
🔴 Critical: > 80 mg/hr — red LED blinks, buzzer sounds, and the button
must be pressed to acknowledge/approve the dose.
Rate limiting — the actual delivered dose ramps toward the target in
small steps rather than jumping instantly, preventing sudden dosage spikes.
Hardware (simulated)
Component
Pin
OLED (SSD1306, I2C)
SDA 21 / SCL 22
Potentiometer
GPIO 34 (analog)
Green LED
GPIO 25
Yellow LED
GPIO 26
Red LED
GPIO 27
Buzzer
GPIO 14
Confirm/Return button
GPIO 12
Repo contents
sketch.ino — main firmware
diagram.json — Wokwi circuit diagram
wokwi.toml — Wokwi simulator config
libraries.txt — required Arduino libraries
secrets.h.example — template for WiFi/Adafruit IO credentials
Setup
Clone the repo.
Copy secrets.h.example to secrets.h and fill in your own WiFi and
Adafruit IO credentials. Never commit
secrets.h — it's already in .gitignore.
Create an Adafruit IO feed named dosage and a slider block (0–100) for
your dashboard.
Open the project in Wokwi (or push to a GitHub repo
and open it via the Wokwi VS Code/GitHub integration), add your own
secrets.h to the simulator project too, and run the simulation.
Install the libraries listed in libraries.txt if building on real
ESP32 hardware in Arduino IDE / PlatformIO.
Safety notes for anyone extending this
The original sketch had a live API key hardcoded in it — that's been moved
into secrets.h so it can be kept out of version control. Rotate any key
that was previously committed anywhere.
If you build on this for something closer to a real device, treat dosage
limits, confirmation logic, and failure states (lost WiFi, sensor faults,
brownout) as safety-critical and get a qualified biomedical engineer
involved — software like this should never control an actual infusion
pump without formal medical-device certification (e.g. IEC 62304).
