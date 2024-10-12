# PiezoDolphin
raspberry pi &amp; piezoelectric BOX

What You'll Need:

    Raspberry Pi (any model, but Pi 3 or 4 recommended)
    Piezoelectric Speaker (also called a piezo buzzer)
    Jumper Wires (for connecting the piezo to the GPIO pins)
    Breadboard (optional, but helpful for easy wiring)
    Resistor (optional, 100Ω or 1kΩ, to limit current and protect the GPIO pin)
    Python (for coding the ultrasonic tone generation)



basic manual. i summarized it, any missing steps are easily discoverable online or you can reach out to me on here*
+++++++++++++++++++++++++++++++++++++++++++++



Here’s an **all-in-one guide** for setting up and controlling a **piezoelectric speaker** with a **Raspberry Pi** to generate ultrasonic sounds, formatted for easy use in the **nano** editor.

---

#### **Part 1: Setting Up the Hardware**

##### Wiring the Piezoelectric Speaker:
1. **Get your components ready:**
   - Raspberry Pi (e.g., Pi 3 or Pi 4)
   - Piezoelectric speaker (buzzer)
   - Jumper wires
   - Optional: Breadboard and resistor (100Ω or 1kΩ)

2. **Wiring steps:**
   - **Positive (+) pin of the piezo**: Connect this to GPIO18 on the Raspberry Pi.
   - **Negative (-) pin of the piezo**: Connect this to any GND pin on the Raspberry Pi.
   - (Optional) Use a resistor between GPIO18 and the piezo’s positive pin to protect the GPIO pin from too much current.

##### Example GPIO Pin Setup:
- **GPIO18 (Pin 12)** → **Positive Pin** of the piezo
- **GND (Pin 6)** → **Negative Pin** of the piezo

Once the wiring is done, you’re ready to generate ultrasonic tones using the Raspberry Pi.

---

#### **Part 2: Python Script for Generating Ultrasonic Sound**

##### Using Nano to Create the Script:
1. Open the **nano editor** on your Raspberry Pi:
   ```bash
   nano ultrasonic_sound.py
   ```

2. Write the following Python code into **nano** to generate an ultrasonic sound at **22 kHz** using **PWM** (Pulse Width Modulation):

```python
# Import required libraries
import RPi.GPIO as GPIO
import time

# Set up the GPIO mode
GPIO.setmode(GPIO.BCM)  # Use BCM numbering
buzzer_pin = 18         # GPIO18 is used to control the piezo

# Set up the GPIO pin as output
GPIO.setup(buzzer_pin, GPIO.OUT)

# Initialize PWM on the pin (22 kHz frequency for ultrasonic sound)
pwm = GPIO.PWM(buzzer_pin, 22000)  # Set frequency to 22kHz
pwm.start(50)  # Start PWM with a 50% duty cycle (on half the time)

# Loop the sound emission
try:
    print("Emitting ultrasonic sound...")
    while True:
        time.sleep(1)  # Modify the sleep time for how long you want the sound to play

except KeyboardInterrupt:
    pass  # Graceful exit on Ctrl+C

# Stop PWM and clean up GPIO
pwm.stop()
GPIO.cleanup()
```

3. **Save and Exit** nano:
   - Press `CTRL + O` to write the file.
   - Press `Enter` to confirm the filename (`ultrasonic_sound.py`).
   - Press `CTRL + X` to exit the nano editor.

---

#### **Part 3: Running the Python Script**

1. **Make sure your Python script is executable**:
   ```bash
   chmod +x ultrasonic_sound.py
   ```

2. **Run the script**:
   ```bash
   sudo python3 ultrasonic_sound.py
   ```

3. **Stopping the script**:
   - If you want to stop the ultrasonic sound, press `CTRL + C` to interrupt the script.

---

#### **Part 4: Customizing the Frequency**

To change the ultrasonic frequency, modify the frequency value in this line of code:

```python
pwm = GPIO.PWM(buzzer_pin, 22000)  # 22kHz frequency
```

For example:
- **For 18 kHz (audible to some people)**:
  ```python
  pwm = GPIO.PWM(buzzer_pin, 18000)
  ```

- **For 25 kHz (higher ultrasonic)**:
  ```python
  pwm = GPIO.PWM(buzzer_pin, 25000)
  ```

You can modify this value to test different frequencies based on your project requirements.

---

#### **Part 5: Testing and Verification**

Since ultrasonic sound is beyond human hearing, you won’t hear it. To verify that the sound is emitted:
- **Use a smartphone app**: Spectrum analyzers like **Spectroid** (for Android) can visualize sound frequencies.
- **Use an ultrasonic detector**: You can get or build an ultrasonic microphone to check that the sound is being produced.

---

#### **Part 6: Troubleshooting Common Issues**

1. **No Sound from the Piezo**:
   - Check the wiring, especially the connection between GPIO18 and the piezo.
   - Ensure that the Python script is running without errors (`sudo python3 ultrasonic_sound.py`).

2. **Piezo is Audible**:
   - If you hear a sound, the frequency might be below ultrasonic levels. Adjust the frequency to be above 20 kHz.

3. **Error: GPIO already in use**:
   - This can happen if a previous script didn’t clean up the GPIO pins. Reboot the Raspberry Pi or run the following:
     ```bash
     sudo python3 -c "import RPi.GPIO as GPIO; GPIO.cleanup()"
     ```

4. **Permission Denied**:
   - If you get a permission error when running the script, make sure to run it with `sudo`:
     ```bash
     sudo python3 ultrasonic_sound.py
     ```

---

#### **Part 7: Additional Resources**

- **RPi.GPIO Documentation**: Explore advanced GPIO control features.
  ```bash
  man gpio
  ```

- **PWM Tuning**: Adjust duty cycle and frequency using advanced signal modulation techniques.

- **MATLAB or Audacity for Audio Testing**: Use MATLAB or Audacity for creating and modulating ultrasonic frequencies.

- ** i also used Audacity to mess with any pre-recorded vocals/vocals found in discovery to allow for modulation to the desired ultra sonic frequency.
---


To customize or expand your project, experiment with different frequencies, sound patterns, and potentially integrating sensors or external inputs.


---

