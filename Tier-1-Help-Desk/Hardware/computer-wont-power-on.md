# Computer Won't Power On

- **Category:** Hardware
- **Tier:** Tier 1 (Help Desk)
- **Version:** 1.0
- **Last Updated:** May 2, 2026
- **Last Reviewed:** May 2, 2026
- **Applies To:** Windows Desktop Computers, Laptops, All Form Factors
- **Difficulty:** L2 (Intermediate)
- **Estimated Resolution Time:** 15-30 minutes
- **Required Access Level:** Power User
- **Severity:** P1 (Single User, Critical — Computer Unusable)
- **Keywords:** power, won't turn on, dead computer, no lights, no boot, PSU, power supply, hard reset, beep codes
- **Prerequisite Knowledge:** Basic hardware familiarity, ability to safely check power cables and external connections

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

## Common Error Codes

| Code | Meaning |
|------|---------|
| No POST | Power-On Self-Test failed — hardware issue preventing boot |
| Blinking Power LED | Specific pattern indicates hardware fault (varies by manufacturer) |
| Continuous short beeps | Power supply, system board, or RAM problem |
| 1 long, 2 short beeps | Display adapter (graphics card) issue |

---

## Symptom-to-Step Mapping

| If You See This | Skip To |
|-----------------|---------|
| No lights at all, no response | Step 1 |
| Computer turns on then immediately off | Step 2 |
| Power light is on but screen is black | Step 5 |
| Burning smell or unusual sounds | Step 3 (then escalate) |
| Laptop not responding on battery | Step 2 (laptop section) |

---

## Triage Questions

Before starting troubleshooting, ask the user:

1. "When you press the power button, do you see any lights turn on or hear any fans spinning, even briefly?"
2. "Is the computer plugged directly into a wall outlet, or through a power strip or surge protector?"
3. "Did anything unusual happen before this — a power outage, storm, moved the computer, or liquid spill?"
4. "For laptops: have you tried removing the battery (if removable) and running on AC power only?"

---

## Quick Checks (30 seconds)

1. Check if the power cable is firmly plugged into both the wall outlet and the back of the computer — loose cables are the most common cause
2. Check if the wall outlet has power — plug a lamp or phone charger into the same outlet to test
3. If using a power strip or surge protector, check if it is turned on and the reset button has not tripped
4. On laptops: remove the battery (if removable), wait 30 seconds, reinsert, and try powering on again
5. Look for any lights on the computer — a faint LED on the motherboard or power button indicates some power is reaching the system
6. If the computer powers on but the monitor shows no signal, see: [External Monitor Not Detected](./external-monitor-not-detected.md)

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

**What to tell the user:** "Power problems are the most common reason a computer won't turn on. We're going to check every single point where power flows — from the wall to the computer. Over half of 'dead computer' issues are solved just by finding a loose cable or a tripped power strip."

### Step 2: Perform a Hard Reset (Drain Residual Power)
1. Residual electrical charge in capacitors can prevent a computer from powering on
2. For desktop computers:
   - Disconnect the power cable from the back of the computer
   - Press and hold the power button for 30 seconds (this drains capacitors of residual charge)
   - Release the power button
   - Reconnect the power cable
   - Press the power button to turn on the computer normally
3. For laptops:
   - Disconnect the AC adapter from the laptop
   - If the battery is removable: remove the battery
   - If the battery is internal (non-removable): locate the small pinhole reset button on the bottom of the laptop (if available) and insert a paperclip for 10 seconds
   - Press and hold the power button for 30-60 seconds
   - Release the power button
   - Reconnect the AC adapter (and battery if removed)
   - Press the power button to turn on the laptop

**What to tell the user:** "Even when unplugged, your computer holds a small electrical charge in its components — like a water tank that stays pressurized after you turn off the pump. That residual charge can lock up the power circuit. We're going to drain it completely by holding the power button while the computer is unplugged. This is the single most effective fix for a computer that won't start."

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

**What to tell the user:** "The power supply is the component most likely to fail in a desktop computer. It's like the heart — if it stops, nothing else can work. We're going to test if yours is still alive using a simple test. Important: only proceed if you're comfortable with this. Otherwise, this is a job for a technician."

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

**What to tell the user:** "A faulty USB device — like a damaged keyboard or a shorted-out phone charger — can actually prevent your computer from starting. It's like a short circuit that trips the safety switch. We're going to disconnect everything and then add devices back one at a time to find the troublemaker."

### Step 5: Check Monitor and Display Connections
1. If fans spin, lights turn on, and hard drive makes noise but the screen is black, the power issue may be with the display or graphics
2. Check monitor power:
   - Ensure the monitor power cable is connected and the monitor power light is on
   - Monitor power light is amber/orange = monitor has power but no signal from computer
   - Monitor power light is off or no light = no power to monitor
3. Verify the video cable is connected from the monitor to the correct port on the computer:
   - Desktop: ensure the monitor is plugged into the dedicated graphics card (lower ports on the back), not the motherboard ports (upper ports)
4. Try a different video cable (HDMI, DisplayPort, etc.) if available
5. Test the monitor with another computer to confirm the monitor itself works
6. Try connecting a different monitor to the computer to see if it displays
7. On laptops: try the keyboard shortcut to toggle display output — Win + P or Fn + F-key (look for the monitor icon, usually F4, F5, F7, or F8)

**What to tell the user:** "Sometimes the computer is actually running — fans spinning, lights on — but the screen is just not showing anything. This is a display problem, not a power problem. Let's check if your computer is secretly alive and just not talking to the screen."

### Step 6: Inspect Internal Hardware (Advanced)
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
   - RAM (memory sticks): Push down the clips on both ends, remove the stick, and firmly reinsert until the clips click into place
   - Graphics card: Remove and firmly reseat in its PCIe slot
   - Power connectors: Ensure the large 24-pin motherboard power connector and the 4/8-pin CPU power connector are firmly seated
6. Try a minimal boot configuration:
   - Remove all components except the essentials: motherboard, CPU, one stick of RAM, and power supply
   - Disconnect all hard drives, SSDs, optical drives, and extra cards
   - Try to power on with this minimal configuration

**What to tell the user:** "Sometimes a component like a RAM stick or graphics card gets slightly unseated, especially after moving the computer. We're going to open the case and make sure everything is properly connected. Only proceed if you're comfortable with this. If the computer is under warranty, skip this step — contact the manufacturer instead."

### Step 7: Reset BIOS/CMOS
1. Corrupted BIOS/UEFI settings can prevent the computer from completing the power-on process
2. Reset the CMOS (the chip that stores BIOS settings):
   - Method 1 — CMOS Battery Removal:
     - Disconnect power cable and open the computer case
     - Locate the coin-cell battery on the motherboard (typically a CR2032 silver disc)
     - Carefully remove the battery using a non-metal tool
     - Wait 2-3 minutes for all BIOS settings to clear
     - Reinsert the battery (positive side up, usually marked with +)
     - Reconnect power and try to turn on the computer
   - Method 2 — CMOS Jumper (if available):
     - Consult the motherboard manual for the location of the CLR_CMOS or JBAT1 jumper
     - Move the jumper from the default pins (1-2) to the clear pins (2-3)
     - Wait 10 seconds, then move it back to the default position
   - Method 3 — CMOS Button (on some high-end motherboards):
     - Look for a "Clear CMOS" button on the rear I/O panel or on the motherboard itself
     - Press and hold the button for 10 seconds while the computer is unplugged
3. After CMOS reset, the computer may prompt for BIOS setup on first boot — this is normal

**What to tell the user:** "Your computer has a small battery on the motherboard that stores BIOS settings. If these settings get corrupted, the computer may not know how to start up. Resetting them returns everything to factory defaults. This is like a factory reset for your computer's startup process."

---

## Alternative Solutions

If the above steps do not resolve the issue, also try:

- Testing with a different power outlet in a different room (not just a different socket on the same wall plate)
- For laptops: testing with a different compatible AC adapter to rule out charger failure
- Removing the CMOS battery overnight to ensure complete discharge of all capacitors
- Connecting the computer to a UPS (Uninterruptible Power Supply) to rule out inconsistent wall power

---

## Prevention Tips

- Use a surge protector or UPS for your computer and all peripherals
- Avoid placing your computer in areas prone to static electricity or extreme temperatures
- Clean dust from vents and fans every 6 months to prevent overheating-related shutdowns
- Do not overload a single wall outlet with too many devices
- When moving your computer, reseat internal components that may have loosened during transport

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

## Escalation Decision Matrix

| Condition | Action |
|-----------|--------|
| All 7 steps completed, issue persists | Escalate to Tier 2 |
| Paperclip test indicates PSU failure | Escalate — requires PSU replacement by qualified technician |
| Burn marks, bulging capacitors, or visible physical damage | Escalate — potential safety hazard |
| Burning smell, sparks, or unusual sounds when attempting power | Escalate urgently — stop testing immediately |
| Laptop battery is internal and needs replacement | Escalate — requires specialized disassembly |
| The computer is under warranty | Escalate — do not open the case; contact manufacturer |
| Issue started after power surge, lightning storm, or liquid spill | Escalate — likely component damage |

---

## Related Articles

- [External Monitor Not Detected](./external-monitor-not-detected.md) — If the computer powers on but the screen shows no signal
- [Check Cables & Basic Hardware Troubleshooting](../Tier-0-Self-Service/check-cables-hardware.md) — Tier 0: Self-service guide for users
- [BIOS/UEFI Configuration & Hardware Diagnostics](../Tier-2-Technical-Support/bios-uefi-diagnostics.md) — Tier 2: Advanced hardware diagnostics
- [Component-Level Failure Analysis & Bench Testing](../Tier-3-Expert-Engineering/component-failure-analysis.md) — Tier 3: Expert-level hardware analysis

> **Note:** If you are looking for the Tier 0 self-service version of this article, see: [Check Cables & Basic Hardware Troubleshooting](../Tier-0-Self-Service/check-cables-hardware.md) (to be created if not yet present).

---

## FAQ

**Q: Can a dead CMOS battery prevent my computer from turning on?**
**A:** Yes, especially on older systems. A dead CMOS battery can reset BIOS settings to defaults, which may include incorrect boot device order or disabled hardware. The fix is replacing the CR2032 battery (usually costs a few dollars).

**Q: What is the difference between a power supply failure and a motherboard failure?**
**A:** A failed power supply means no power reaches any component — no fans, no lights, no nothing. A failed motherboard may show some signs of life (fans spin, lights on) but the system won't complete POST. The paperclip test in Step 3 helps isolate which one is bad.

**Q: Is it safe to use a different power cable for my computer?**
**A:** Yes, for desktop computers. The IEC C13 power cable (the standard three-prong cable) is universal. For laptops, you must use an AC adapter with the exact same voltage, amperage, and connector size — using the wrong adapter can damage the laptop.

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

---

## Was this article helpful?

If this article helped resolve your issue, great. If something was unclear, missing, or did not work, please open a GitHub Issue describing the problem so we can improve it.

Suggest improvements at: https://github.com/EzioLockhart/Tier-1-Support-Knowledge-Base/issues

---

## References

- CompTIA A+ Troubleshooting Methodology: Identify the problem, Establish a theory, Test the theory, Establish a plan of action, Verify functionality, Document findings
- ITIL Incident Management best practices: Prioritize based on impact and urgency
- Manufacturer-specific diagnostic beep code documentation (Dell, HP, Lenovo, ASUS, Gigabyte)

---

*Tier: Tier 1 (Help Desk) | Difficulty: L2 (Intermediate) | Estimated Resolution Time: 15-30 minutes | Required Access Level: Power User | Severity: P1 (Single User Critical)*

---

For internal use. Follow your organization's hardware support and warranty policies. Do not open sealed systems that are under warranty.
