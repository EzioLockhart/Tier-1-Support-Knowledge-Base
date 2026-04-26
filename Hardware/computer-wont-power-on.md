# Computer Won't Power On

**Category:** Hardware
**Last Updated:** April 27, 2026
**Applies To:** Windows Desktop Computers, Laptops, All Form Factors

---

## Symptoms

- Pressing the power button does nothing — no lights, no fans, no sounds
- Computer briefly turns on (fans spin, lights flash) then immediately turns off
- Power light on the computer is on but the screen remains completely black
- Laptop does not respond when pressing the power button even when plugged in
- Computer was working normally but suddenly will not power on after a shutdown or restart
- Burning smell, unusual clicking noise, or visible sparks came from the computer before it stopped powering on
- Power LED blinks in a specific pattern (consult manufacturer documentation for blink codes)

---

## Quick Checks (30 seconds)

1. Check if the power cable is firmly plugged into both the wall outlet and the back of the computer — loose cables are the most common cause
2. Check if the wall outlet has power — plug a lamp or phone charger into the same outlet to test
3. If using a power strip or surge protector, check if it is turned on and the reset button has not tripped
4. On laptops: remove the battery (if removable), wait 30 seconds, reinsert, and try powering on again
5. Look for any lights on the computer — a faint LED on the motherboard or power button indicates some power is reaching the system

---

## Step-by-Step Resolution

### Step 1: Check Power Source and Cables

1. Verify the wall outlet works by plugging in a known-working device (lamp, phone charger, monitor)
2. If using a power strip or surge protector:
   - Ensure the power strip's switch is in the ON position
   - Check if the surge protector's reset button has tripped — press the reset button
   - Try plugging the computer directly into the wall outlet to bypass the power strip entirely
3. Check the power cable connections:
   - The cable must be firmly inserted at both ends (wall and computer)
   - For desktop computers: check both ends of the power cable
   - For laptops: check the AC adapter connection at the laptop and the "brick" connection in the middle of the cable
4. Inspect the power cable for visible damage:
   - Cuts, frays, kinks, or exposed wires in the cable
   - Bent or broken pins in the connector
   - Loose connection where the cable enters the plug housing
5. If available, try a different power cable of the same type (IEC C13 for most desktops, specific AC adapter for laptops)
6. Try a different wall outlet in a different room to rule out a faulty electrical circuit
   - Power delivery issues account for over 50% of "computer won't power on" scenarios; always eliminate power source and cable problems first.

### Step 2: Perform a Hard Reset (Drain Residual Power)

1. Residual electrical charge in capacitors can prevent a computer from powering on
2. For **desktop computers:**
   - Disconnect the power cable from the back of the computer
   - Press and hold the **power button** for 30 seconds (this drains capacitors of residual charge)
   - Release the power button
   - Reconnect the power cable
   - Press the power button to turn on the computer normally
3. For **laptops:**
   - Disconnect the AC adapter from the laptop
   - If the battery is removable: remove the battery
   - If the battery is internal (non-removable): locate the small pinhole reset button on the bottom of the laptop (if available) and insert a paperclip for 10 seconds
   - Press and hold the **power button** for 30-60 seconds
   - Release the power button
   - Reconnect the AC adapter (and battery if removed)
   - Press the power button to turn on the laptop
4. If the computer powers on after this procedure, the issue was residual charge buildup
   - Hard reset resolves more "no power" issues than any other single step because residual charge in capacitors can lock the power circuit.

### Step 3: Check the Power Supply Unit (Desktop Computers)

1. The Power Supply Unit (PSU) converts wall power to voltages the computer components can use; a failed PSU means no power at all
2. Check for signs of PSU failure:
   - No fan spin or lights at all when power button is pressed
   - Brief fan spin for half a second then stops (PSU protection circuit tripping)
   - Burning smell from the back of the computer near the power cable inlet
3. Perform the paperclip test (only for users comfortable with basic hardware testing):
   - Disconnect the power cable from the PSU
   - Turn off the PSU switch (if it has one) to the OFF (0) position
   - Disconnect all PSU cables from the motherboard and components
   - Take a standard metal paperclip and bend it into a U-shape
   - Locate the 24-pin motherboard connector: find the green wire (pin 16, PS_ON) and any black wire (ground, e.g., pin 15 or 17)
   - Insert one end of the paperclip into the green wire pin and the other end into the black wire pin
   - Ensure the paperclip is not touching any other pins
   - Plug in the power cable and switch the PSU to ON (1)
   - If the PSU fan spins, the PSU is providing power (but may still be faulty under load)
   - If nothing happens, the PSU is likely dead and needs replacement
4. If uncomfortable with the paperclip test, skip it and test with a known-working PSU if available
   - The power supply is one of the most common hardware failure points; if all external power checks pass and the hard reset fails, PSU failure is highly likely.

### Step 4: Disconnect All Peripherals and External Devices

1. A faulty external device or peripheral can cause a short circuit or power drain that prevents the computer from booting
2. Disconnect everything from the computer except the power cable:
   - USB devices (keyboard, mouse, external drives, webcam, printer, USB hubs)
   - Monitor cables (HDMI, DisplayPort, VGA, DVI)
   - Audio cables (speakers, headphones, microphone)
   - Network cable (Ethernet)
   - Any other device plugged into any port
3. For desktop computers: also disconnect internal front panel USB, audio, and card reader connectors from the motherboard if accessible
4. Once everything is disconnected, try powering on the computer
5. If the computer powers on:
   - A connected device or cable is causing the problem
   - Reconnect devices one at a time, testing power after each reconnection
   - When the computer fails to power on again, the last device reconnected is the culprit
6. If the computer still does not power on with everything disconnected, the problem is internal (PSU, motherboard, or internal component)
   - A shorted USB port, faulty keyboard, or damaged cable can prevent an otherwise healthy computer from powering on.

### Step 5: Check Monitor and Display Connections (If Computer Seems to Power On but Screen Is Black)

1. If fans spin, lights turn on, and hard drive makes noise but the screen is black, the power issue may be with the display or graphics
2. Check monitor power:
   - Ensure the monitor power cable is connected and the monitor power light is on
   - Monitor power light is amber/orange = monitor has power but no signal from computer
   - Monitor power light is off or no light = no power to monitor
3. Verify the video cable is connected from the monitor to the correct port on the computer:
   - Desktop: ensure the monitor is plugged into the dedicated graphics card (lower ports on the back), not the motherboard ports (upper ports)
   - If the computer has both a graphics card and motherboard video ports, a monitor connected to the motherboard port will show a black screen if the graphics card is primary
4. Try a different video cable (HDMI, DisplayPort, etc.) if available
5. Test the monitor with another computer to confirm the monitor itself works
6. Try connecting a different monitor to the computer to see if it displays
7. On laptops: try the keyboard shortcut to toggle display output — **Win + P** or **Fn + F-key** (look for the monitor icon on the function keys, usually F4, F5, F7, or F8)
   - A computer that powers on but has no display is a different problem from "no power"; always verify if the computer is actually running by listening for fan noise and checking internal lights.

### Step 6: Inspect Internal Hardware (Desktop Computers — Advanced)

1. Only perform internal inspection if you are comfortable opening the computer case and the warranty allows it
2. Before opening the case:
   - Disconnect the power cable completely
   - Press and hold the power button for 10 seconds to discharge any remaining power
   - Wear an anti-static wrist strap if available, or touch a metal part of the case to ground yourself
3. Open the computer case
4. Visually inspect the motherboard for:
   - Blown, bulging, or leaking capacitors (capacitors are small cylindrical components; failed ones bulge at the top or leak brown fluid)
   - Burn marks, scorching, or melted areas on the motherboard or components
   - Loose cables or connectors
5. Reseat key components:
   - **RAM (memory sticks):** Push down the clips on both ends, remove the stick, and firmly reinsert until the clips click into place
   - **Graphics card:** Remove and firmly reseat in its PCIe slot
   - **Power connectors:** Ensure the large 24-pin motherboard power connector and the 4/8-pin CPU power connector near the processor are firmly seated
   - **Data cables:** Ensure SATA cables connecting hard drives and SSDs are secure
6. Try a minimal boot configuration:
   - Remove all components except the essentials: motherboard, CPU, one stick of RAM, and power supply
   - Disconnect all hard drives, SSDs, optical drives, and extra cards
   - Try to power on with this minimal configuration
   - If it powers on, re-add components one at a time until the faulty component is identified
7. Listen for beep codes when powering on:
   - Most motherboards emit a series of beeps to indicate hardware problems
   - Count the number of beeps (e.g., 1 short beep usually means normal POST, continuous beeps usually mean RAM issue)
   - Look up the beep code pattern for your specific motherboard or computer manufacturer
   - A faulty RAM stick or loose RAM is one of the most common reasons a computer powers on but fails to boot; reseating RAM resolves this frequently.

### Step 7: Reset BIOS/CMOS

1. Corrupted BIOS/UEFI settings can prevent the computer from completing the power-on process
2. Reset the CMOS (the chip that stores BIOS settings):
   - **Method 1 — CMOS Battery Removal:**
     - Disconnect power cable and open the computer case
     - Locate the coin-cell battery on the motherboard (typically a CR2032 silver disc)
     - Carefully remove the battery using a non-metal tool
     - Wait 2-3 minutes for all BIOS settings to clear
     - Reinsert the battery (positive side up, usually marked with +)
     - Reconnect power and try to turn on the computer
   - **Method 2 — CMOS Jumper (if available):**
     - Consult the motherboard manual for the location of the CLR_CMOS or JBAT1 jumper
     - Move the jumper from the default pins (1-2) to the clear pins (2-3)
     - Wait 10 seconds, then move it back to the default position
     - Reconnect power and test
   - **Method 3 — CMOS Button (on some high-end motherboards):**
     - Look for a "Clear CMOS" button on the rear I/O panel or on the motherboard itself
     - Press and hold the button for 10 seconds while the computer is unplugged
3. After CMOS reset, the computer may prompt for BIOS setup on first boot — this is normal
4. The date and time will need to be set again
   - CMOS reset returns BIOS settings to factory defaults, clearing any misconfiguration that could prevent power-on.

---

## Root Cause

Common causes of computer not powering on, in order of likelihood:

- Loose or faulty power cable, power strip turned off, or dead wall outlet (most common — always check connections first)
- Residual electrical charge in capacitors preventing power circuit activation (resolved by hard reset)
- Failed Power Supply Unit (PSU) — especially common on desktop computers older than 3-5 years
- Faulty external device or peripheral causing a short circuit
- Dead or completely discharged laptop battery combined with a faulty AC adapter
- Overheating causing automatic shutdown and refusal to restart until cooled down
- Loose internal component (RAM, graphics card, power connector) — especially after moving the computer
- Motherboard failure (blown capacitors, short circuit, or component failure) — least common but most serious

---

## Escalation Criteria

Escalate to Tier 2 / Hardware Repair Team if:

- Paperclip test indicates PSU failure — requires PSU replacement by qualified technician
- Burn marks, bulging capacitors, or visible physical damage found on the motherboard
- Computer emits burning smell, sparks, or unusual sounds when attempting to power on — stop testing immediately, potential electrical hazard
- Laptop battery is internal and needs replacement — requires specialized disassembly
- All troubleshooting steps exhausted and computer still does not power on — likely motherboard failure
- The computer is under warranty — do not open the case; escalate to manufacturer service
- User reports the issue started after a power surge, lightning storm, or liquid spill

---

## Diagnostic Beep Codes Quick Reference

| Beep Pattern | Common Meaning |
|--------------|----------------|
| 1 short beep | Normal POST — computer passed hardware check |
| Continuous short beeps | Power supply, system board, or RAM problem |
| 1 long, 2 short beeps | Display adapter (graphics card) issue |
| 1 long, 3 short beeps | Keyboard controller or RAM issue |
| Repeated long beeps | RAM not detected or memory error |
| 2 short beeps | CMOS setting error (configuration mismatch) |
| No beeps at all | Power supply, motherboard, or CPU failure |

*Note: Beep codes vary by manufacturer (Dell, HP, Lenovo, ASUS, Gigabyte, etc.). Consult your specific model's documentation.*

---

For internal use. Follow your organization's hardware support and warranty policies. Do not open sealed systems that are under warranty.
