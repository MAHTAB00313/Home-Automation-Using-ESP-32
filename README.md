# Home-Automation-Using-ESP-32
Home Automation System using Blynk and ESP32. Control appliances remotely via smartphone app or manually with push buttons. Monitors smoke levels for safety, providing real-time alerts. Enhances convenience and safety in residential environments.

Components Used
  1. ESP32 development board
  2. Blynk app (installed on smartphone)
  3. WiFi network
  4. Home appliances (e.g., bulbs, fans)
  5. Smoke sensor module
  6. Push buttons
  7. Connecting wires

Setup Instructions

Hardware Setup:
  1. Connect the ESP32 to your WiFi network by updating ssid and pass variables in the code with your WiFi credentials.
  2. Wire the home appliances to relays connected to the ESP32 GPIO pins (bulb_relay, fan_relay).
  3. Connect the smoke sensor to the ESP32 (smokeSensor pin) and fire system indicator (fireSystem pin).

Software Setup:
  
  1. Install the Arduino IDE on your computer if not already installed.
  2. Clone or download the project repository from GitHub.
  3. Open the Arduino IDE, navigate to File -> Open, and open the .ino file from the downloaded repository.
  4. Replace BLYNK_AUTH_TOKEN with your Blynk authentication token from the Blynk app.
  5. Update ssid and pass variables in the code with your WiFi credentials.

Upload Code to ESP32:

  1. Select the correct board and COM port from Tools menu in Arduino IDE.
  2. Click on the upload button to compile and upload the code to the ESP32.

Configure Blynk App:

  1. Download and install the Blynk app from Google Play Store or Apple App Store.
  2. Create a new project in the Blynk app.
  3. Select ESP32 as the device and connect it to your Blynk project using the provided Auth Token (BLYNK_AUTH_TOKEN).

Launch the Blynk app and start controlling appliances:
  1. Use virtual buttons (bulb_vpin, fan_vpin) in the Blynk app to toggle appliances remotely.
  2. Press physical push buttons (bulb_btn, fan_btn) connected to the ESP32 for manual control.

Monitor smoke levels:
  1. View real-time smoke sensor data (smokeGuage_vpin) on the Blynk app.
  2. Receive alerts if smoke levels exceed safe thresholds.

Deployment:

  1. Install the ESP32 and connected components in a suitable location within your home.
  2. Ensure the ESP32 is powered and connected to the WiFi network for continuous operation.
  3. Test the system thoroughly to ensure proper functionality of remote and manual controls, as well as smoke monitoring.


Additional Notes
  1. Ensure the Blynk app remains connected to the ESP32 and has access to the internet for remote operations.
  2. Calibrate the smoke sensor as per manufacturer instructions to ensure accurate readings.
  3. Adjust GPIO pin assignments in the code if different pins are used for components.


