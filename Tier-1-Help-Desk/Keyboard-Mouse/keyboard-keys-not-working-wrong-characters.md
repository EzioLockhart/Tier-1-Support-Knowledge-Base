# Keyboard Keys Not Working or Typing Wrong Characters

- **Category:** Keyboard & Mouse
- **Tier:** Tier 1 (Help Desk)
- **Version:** 1.0
- **Last Updated:** May 2, 2026
- **Last Reviewed:** May 2, 2026
- **Applies To:** Windows 10 (22H2), Windows 11 (23H2), All Keyboard Types (Built-in, USB, Wireless, Bluetooth)
- **Difficulty:** L1 (Basic)
- **Estimated Resolution Time:** 10-15 minutes
- **Required Access Level:** User
- **Severity:** P2 (Single User, Degraded — Input Difficulty)
- **Keywords:** keyboard, keys, not working, wrong characters, typing, layout, language, driver, Bluetooth, USB
- **Prerequisite Knowledge:** Basic Windows navigation, ability to access Settings

---

## Symptoms

- Specific keys do not respond when pressed
- Keyboard types wrong characters (e.g., @ instead of ", pound instead of dollar)
- Keyboard types numbers instead of letters
- Laptop built-in keyboard not working but external keyboard works
- Wireless or Bluetooth keyboard not connecting or keeps disconnecting
- Keyboard works in some applications but not others
- Sticky keys, Filter Keys, or other accessibility features activated unintentionally

---

## Common Error Codes

| Code | Meaning |
|------|---------|
| Event ID 19 | Keyboard device driver error — driver conflict or corruption |
| 0x8007001F | Device malfunction — keyboard not responding to driver requests |
| Code 10 | Device cannot start — driver or hardware issue in Device Manager |
| Code 43 | Device reported a problem and was stopped — common with Bluetooth keyboards |

---

## Symptom-to-Step Mapping

| If You See This | Skip To |
|-----------------|---------|
| Keyboard types wrong characters consistently | Step 1 |
| Specific keys not working at all | Step 2 |
| Laptop keyboard not working | Step 3 |
| Wireless/Bluetooth keyboard disconnected | Step 4 |
| Keyboard types numbers instead of letters | Step 5 |

---

## Triage Questions

Before starting troubleshooting, ask the user:

1. "Is this a built-in laptop keyboard, a USB keyboard, or a wireless/Bluetooth keyboard?"
2. "Are all keys not working, or just specific ones?"
3. "Did this start after anything spilled on the keyboard or after the laptop was dropped?"
4. "When you press a key, does it type the wrong character, or nothing at all?"

---

## Quick Checks (30 seconds)

1. Restart the computer — this clears temporary driver glitches that can cause keyboard issues
2. Try connecting a different keyboard (USB or Bluetooth) to determine if the issue is the keyboard or the computer
3. Check if Num Lock is on (common on compact keyboards where letters double as number pads)
4. Check if Sticky Keys or Filter Keys are enabled: rapidly press Shift 5 times — if a dialog appears, accessibility features are on
5. Look for debris, crumbs, or liquid residue around the affected keys
6. If you need quick fixes for both keyboard and mouse, see: [Troubleshoot Keyboard & Mouse — Quick Fixes](../Tier-0-Self-Service/troubleshoot-keyboard-mouse.md)

---

## Step-by-Step Resolution

### Step 1: Check Keyboard Language and Layout Settings
1. The most common cause of wrong characters is incorrect keyboard layout
2. Check the current layout: look at the system tray for the language icon (e.g., ENG, FRA, or a keyboard icon)
3. Click the language icon and ensure the correct language is selected
4. If multiple layouts are present, remove the incorrect ones:
   - Settings > Time & language > Language & region
   - Under "Preferred languages", click the three dots next to any unwanted language > "Remove"
5. Check keyboard layout within the correct language:
   - Click the three dots next to your language > "Language options"
   - Under "Keyboards", ensure the correct layout is listed (e.g., US QWERTY, UK QWERTY)
   - Remove any incorrect layouts by clicking the three dots > "Remove"
6. The difference between US and UK layouts: US has @ above 2, UK has " above 2. This is a very common confusion.

**What to tell the user:** "Your computer might be set to the wrong keyboard language — like thinking you have a UK keyboard when you actually have a US one. This is the most common reason keys type the wrong characters. Let's check which layout Windows thinks your keyboard is using."

### Step 2: Clean the Keyboard and Check for Physical Obstruction
1. For external keyboards:
   - Unplug the keyboard
   - Turn it upside down and gently shake to dislodge crumbs and debris
   - Use compressed air to blow out dust between keys
   - Wipe keycaps with a slightly damp microfiber cloth
   - Check for any keys that feel stuck or different from others when pressed
2. For laptop keyboards:
   - Power off the laptop completely
   - Use compressed air at an angle to blow debris out from under keys
   - Gently clean around keys with a soft brush
   - Do not use liquids directly on the keyboard
3. If keys are sticking due to liquid spill:
   - Power off immediately and unplug
   - Tilt the keyboard to drain liquid away from the electronics
   - Let it dry completely (24-48 hours) before testing
4. Reconnect and test the keyboard

**What to tell the user:** "Dust, crumbs, and debris are the second most common cause of keyboard problems. Even a tiny crumb under a key can prevent it from pressing down fully. Let's give your keyboard a thorough cleaning and see which keys come back to life."

### Step 3: Reinstall the Keyboard Driver
1. A corrupted driver can cause the entire keyboard or specific keys to stop working
2. Press Win + X > Device Manager
3. Expand "Keyboards" — you should see your keyboard listed (e.g., "HID Keyboard Device", "Standard PS/2 Keyboard")
4. Right-click the keyboard > "Uninstall device"
5. If multiple keyboard entries exist (common on laptops with built-in + external), uninstall all of them
6. Restart the computer — Windows will automatically reinstall the correct drivers
7. For laptop keyboards specifically, also check under "System devices" for any keyboard controller or filter driver
8. After restart, test all keys

**What to tell the user:** "The keyboard driver is the translator between your physical key presses and what Windows understands. If this driver gets corrupted, Windows misinterprets your keystrokes or ignores them completely. Uninstalling and restarting forces Windows to install a fresh, clean driver."

### Step 4: Troubleshoot Wireless and Bluetooth Keyboards
1. For USB wireless keyboards (with a dongle):
   - Unplug the USB receiver, wait 10 seconds, and plug it into a different USB port
   - Avoid USB hubs — connect directly to the computer
   - Check the keyboard batteries — low batteries cause intermittent failures
   - Press the "Connect" or "Pair" button on the keyboard and receiver
2. For Bluetooth keyboards:
   - Ensure Bluetooth is ON: Settings > Bluetooth & devices > toggle ON
   - Remove the keyboard: Settings > Bluetooth & devices > find keyboard > three dots > "Remove device"
   - Put the keyboard into pairing mode (check manufacturer instructions — usually hold a specific button for 3-5 seconds)
   - Click "Add device" > "Bluetooth" > select your keyboard when it appears
   - Ensure the keyboard has fresh or charged batteries
3. Check for wireless interference: move the keyboard closer to the computer, away from metal objects and other wireless devices

**What to tell the user:** "Wireless keyboards rely on either a USB receiver or Bluetooth. If the connection drops, it might look like the keyboard is broken when it's actually just disconnected. For Bluetooth keyboards especially, removing and re-pairing often fixes persistent connection issues."

### Step 5: Disable Accessibility Features (Sticky Keys, Filter Keys, Toggle Keys)
1. Windows accessibility features can change how the keyboard behaves
2. Sticky Keys: makes modifier keys (Shift, Ctrl, Alt) stay active without holding them — causes unexpected behavior
3. Filter Keys: ignores brief or repeated keystrokes — makes keys seem unresponsive
4. Toggle Keys: plays a sound when Caps Lock, Num Lock, or Scroll Lock are pressed
5. To disable all:
   - Settings > Accessibility > Keyboard
   - Turn OFF "Sticky keys", "Filter keys", and "Toggle keys"
   - Uncheck "Allow the shortcut key to start Sticky Keys" and similar for Filter Keys and Toggle Keys
6. Also check if Num Lock is causing the issue:
   - On compact laptops, the right side of the keyboard may double as a number pad when Num Lock is on
   - Press the Num Lock key (often Fn + a function key) to toggle
   - Test if letters now type correctly

**What to tell the user:** "Windows has accessibility features designed to help people with motor difficulties, but they can be turned on accidentally — usually by holding a key too long or pressing Shift repeatedly. These features change how your keyboard behaves. Let's make sure they're all turned off."

### Step 6: Check for Conflicting Software and Perform Clean Boot
1. Some third-party software can intercept keyboard input (gaming software, macro programs, keyboard customization tools)
2. Check if any keyboard-related software is installed:
   - Look in the system tray for keyboard software icons (Razer Synapse, Logitech G Hub, Corsair iCUE, etc.)
   - These programs can remap keys or create macros that interfere with normal typing
3. Temporarily exit or disable such software and test the keyboard
4. If unsure which software is causing the issue, perform a clean boot:
   - Press Win + R > type msconfig > Enter
   - Go to "Services" tab > check "Hide all Microsoft services" > "Disable all"
   - Go to "Startup" tab > "Open Task Manager" > disable all startup items
   - Restart the computer and test the keyboard
5. If the keyboard works in clean boot, a third-party program is the cause
6. Re-enable services and startup items in small groups to find the culprit

**What to tell the user:** "Software that came with your keyboard — especially gaming keyboards — can reprogram what each key does. A key that types 'W' might be set to type '1' instead. We're going to check for keyboard software and disable it temporarily to see if that's causing your problem."

---

## Alternative Solutions

If the above steps do not resolve the issue, also try:

- Testing the keyboard on a different computer to determine if the keyboard itself is faulty
- Using the Windows On-Screen Keyboard (Start > type "On-Screen Keyboard") as a temporary workaround
- Checking for BIOS updates from your laptop or motherboard manufacturer that address keyboard issues
- Connecting an external USB keyboard to a laptop with a broken built-in keyboard as an immediate fix

---

## Prevention Tips

- Clean your keyboard regularly with compressed air to prevent debris buildup under keys
- Keep liquids away from your keyboard — use a spill-proof container
- For wireless keyboards, replace batteries before they fully die (low battery causes erratic behavior)
- Avoid eating over your keyboard to prevent crumbs from getting under keys
- Update keyboard drivers and firmware through your manufacturer's software

---

## Root Cause

Common causes of keyboard issues, in order of likelihood:

- Incorrect keyboard language or layout selected in Windows (most common)
- Debris, crumbs, or dust under keys causing physical obstruction
- Corrupted or outdated keyboard driver
- Wireless connection lost or Bluetooth pairing broken
- Accessibility features (Sticky Keys, Filter Keys, Num Lock) accidentally enabled
- Third-party keyboard software remapping keys or intercepting input
- Physical damage from liquid spill or impact
- Hardware failure in the keyboard itself (least common but requires replacement)

---

## Escalation Decision Matrix

| Condition | Action |
|-----------|--------|
| All 6 steps completed, issue persists | Escalate to Tier 2 |
| Keyboard not detected in Device Manager at all | Escalate — possible motherboard or USB controller issue |
| Liquid spill confirmed on laptop keyboard | Escalate — requires hardware inspection |
| Keys physically broken or missing keycaps | Escalate — requires keyboard replacement |
| External keyboard works but built-in keyboard does not | Escalate — likely hardware issue with built-in keyboard |
| Keyboard works on another computer without issue | Escalate — possible computer hardware or port issue |
| Language layout or driver reinstall resolves the issue | Do not escalate — document solution |

---

## Related Articles

- [Troubleshoot Keyboard & Mouse — Quick Fixes](../Tier-0-Self-Service/troubleshoot-keyboard-mouse.md) — Tier 0: Self-service keyboard fixes
- [Bluetooth HID Stack Diagnostics & Reconnection Issues](../Tier-2-Technical-Support/bluetooth-hid-stack.md) — Tier 2: Advanced Bluetooth diagnostics
- [Input Device Driver Architecture & Filter Driver Analysis](../Tier-3-Expert-Engineering/input-driver-architecture.md) — Tier 3: Expert input analysis

> **Note:** The following related articles are planned for future creation within their respective tier folders:
> - [Troubleshoot Keyboard & Mouse — Quick Fixes](../Tier-0-Self-Service/troubleshoot-keyboard-mouse.md)
> - [Bluetooth HID Stack Diagnostics & Reconnection Issues](../Tier-2-Technical-Support/bluetooth-hid-stack.md)
> - [Input Device Driver Architecture & Filter Driver Analysis](../Tier-3-Expert-Engineering/input-driver-architecture.md)

---

## FAQ

**Q: Why does my keyboard type the wrong characters only in certain applications?**
**A:** This usually means the application has its own keyboard language setting that overrides Windows. Check the application's language or input settings. Some apps (especially older ones) do not support Unicode and may misinterpret your keyboard layout.

**Q: How do I type if my keyboard is completely broken?**
**A:** Use the On-Screen Keyboard: Start menu > type "On-Screen Keyboard" and launch it. You can click keys with your mouse. As a longer-term solution, connect any USB or Bluetooth keyboard to your laptop.

**Q: Can I remap a broken key to another key?**
**A:** Yes. Microsoft PowerToys (free from Microsoft) includes a Keyboard Manager that lets you remap any key to any other key. For example, if your 'A' key is broken, you can remap the rarely-used 'Scroll Lock' key to type 'A'.

---

## Keyboard Troubleshooting Quick Reference

| Issue | Quick Check |
|-------|-------------|
| Wrong characters | Check language in system tray (ENG, UK, etc.) |
| Numbers instead of letters | Check Num Lock status |
| Keys not responding | Check Sticky Keys and Filter Keys in Accessibility settings |
| Bluetooth keyboard disconnected | Remove and re-pair in Bluetooth settings |
| Specific key dead | Clean under keycap with compressed air |

---

## Was this article helpful?

If this article helped resolve your issue, great. If something was unclear, missing, or did not work, please open a GitHub Issue describing the problem so we can improve it.

Suggest improvements at: https://github.com/EzioLockhart/Complete-IT-Support-Knowledge-Base-Tier-0-to-Tier-3/issues

---

## References

- CompTIA A+ Troubleshooting Methodology: Identify the problem, Establish a theory, Test the theory, Establish a plan of action, Verify functionality, Document findings
- ITIL Incident Management best practices: Prioritize based on impact and urgency
- Microsoft official documentation: Troubleshoot keyboard issues in Windows

---

*Tier: Tier 1 (Help Desk) | Difficulty: L1 (Basic) | Estimated Resolution Time: 10-15 minutes | Required Access Level: User | Severity: P2 (Single User Degraded)*

---

For internal use. Follow your organization's hardware support and replacement policies.
