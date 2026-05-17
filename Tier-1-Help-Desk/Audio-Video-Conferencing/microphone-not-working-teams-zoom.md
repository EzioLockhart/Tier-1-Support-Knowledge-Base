# Microphone Not Working in Teams or Zoom

- **Category:** Audio & Video Conferencing
- **Tier:** Tier 1 (Help Desk)
- **Version:** 1.0
- **Last Updated:** May 2, 2026
- **Last Reviewed:** May 2, 2026
- **Applies To:** Microsoft Teams, Zoom, Windows 10 (22H2), Windows 11 (23H2), macOS
- **Difficulty:** L1 (Basic)
- **Estimated Resolution Time:** 10-15 minutes
- **Required Access Level:** User
- **Severity:** P1 (Single User, Critical — Cannot Participate in Meetings)
- **Keywords:** microphone, Teams, Zoom, audio, mute, not working, permissions, device, input
- **Prerequisite Knowledge:** Basic Windows navigation, ability to access Settings and app permissions

---

## Symptoms

- Other meeting participants cannot hear you
- Microphone icon shows muted even when you are not muted
- "No microphone detected" or "Microphone not found" error in Teams or Zoom
- Microphone works in other applications but not in Teams or Zoom
- Audio is choppy, cutting out, or sounds robotic to others
- Microphone test shows no input or very low volume
- The microphone device does not appear in the app's audio settings

---

## Common Error Codes

| Code | Meaning |
|------|---------|
| 0x80070005 | Access denied — app does not have microphone permission |
| Event ID 17 | Audio device error — driver or hardware issue |
| No input device found | Operating system or app cannot detect any microphone |
| ERR_AUDIO_INPUT | Browser-based Teams/Zoom cannot access microphone |

---

## Symptom-to-Step Mapping

| If You See This | Skip To |
|-----------------|---------|
| Microphone works in other apps but not Teams/Zoom | Step 2 |
| "No microphone detected" error | Step 3 |
| Microphone too quiet or robotic sound | Step 4 |
| Using external USB/Bluetooth microphone | Step 5 |
| Microphone stopped working after Windows Update | Step 6 |

---

## Triage Questions

Before starting troubleshooting, ask the user:

1. "Is this a built-in laptop microphone, a headset, or an external USB microphone?"
2. "Does the microphone work in other applications, like Voice Recorder or a different meeting app?"
3. "When did this problem start — has it ever worked before?"
4. "Are you using the desktop app or the web browser version of Teams/Zoom?"

---

## Quick Checks (30 seconds)

1. Check if you are muted in the meeting — look for the microphone icon with a slash through it and click to unmute
2. Verify the correct microphone is selected in the app: Teams > Settings > Devices; Zoom > Settings > Audio
3. Try the "Make a test call" feature: Teams > Settings > Devices > Make a test call; Zoom > Settings > Audio > Test Mic
4. Check physical mute buttons on your headset or external microphone
5. Restart the Teams or Zoom app completely — close from system tray, not just the window
6. If your camera also is not working, see: [Fix Microphone & Camera Issues — Quick Check](../Tier-0-Self-Service/fix-mic-camera-issues.md)

---

## Step-by-Step Resolution

### Step 1: Check Windows Microphone Settings
1. Right-click the speaker icon in the system tray > "Sound settings"
2. Under "Input", verify the correct microphone is selected from the dropdown
3. Speak into your microphone and check the "Test your microphone" bar — it should move as you speak
4. If the bar does not move, the microphone is not being detected at all
5. Click "Device properties" or "Microphone properties" under the input selection
6. Ensure the volume slider is set to at least 80%
7. Go to "Additional device properties" > "Levels" tab > set Microphone to 100 and Microphone Boost to +20 dB if available
8. Go to the "Advanced" tab > uncheck "Allow applications to take exclusive control of this device"

**What to tell the user:** "Windows controls which microphone all your apps use. If the wrong microphone is selected here, no app will hear you correctly. Let's check the Windows sound settings first because they override everything else."

### Step 2: Check App Permissions for Microphone Access
1. Windows privacy settings can block apps from using the microphone
2. Open Settings > Privacy & Security > Microphone
3. Ensure "Microphone access" is turned ON
4. Ensure "Let apps access your microphone" is turned ON
5. Scroll down to the list of apps and ensure Teams and Zoom are both ON
6. If using the web browser version, also ensure your browser (Chrome, Edge) is ON in the list
7. Restart the Teams or Zoom app after changing any permissions
8. For macOS: System Preferences > Security & Privacy > Privacy > Microphone > check Teams and Zoom

**What to tell the user:** "Windows has a privacy feature that can block apps from using your microphone. Even if the microphone works in Windows, individual apps can be blocked. Let's make sure Teams and Zoom are allowed to access your microphone."

### Step 3: Select the Correct Microphone in the App
1. The app may be trying to use a different microphone than the one you are speaking into
2. Microsoft Teams:
   - Click the three dots (...) next to your profile > Settings > Devices
   - Under "Audio devices", check the "Microphone" dropdown
   - Select your intended microphone from the list
   - Click "Make a test call" to verify it works
3. Zoom:
   - Click the gear icon (Settings) > Audio
   - Under "Microphone", select your device from the dropdown
   - Click "Test Mic" and speak — you should hear your voice played back
   - Adjust the "Input Volume" slider if too quiet or loud
4. If your microphone does not appear in the list at all, the device is not being recognized — proceed to Step 5

**What to tell the user:** "Teams and Zoom may be trying to use a different microphone — like your webcam's built-in mic instead of your headset. Let's look at which microphone each app is actually using and switch to the right one."

### Step 4: Run Windows Audio Troubleshooter
1. Windows has a built-in diagnostic tool for audio issues
2. Open Settings > System > Troubleshoot > Other troubleshooters
   - On Windows 10: Settings > Update & Security > Troubleshoot > Additional troubleshooters
3. Find "Recording Audio" in the list and click "Run"
4. Select your microphone device when prompted
5. Follow the on-screen recommendations and apply any fixes
6. The troubleshooter checks for driver issues, disabled devices, and volume settings
7. Restart your computer after the troubleshooter completes
8. Test your microphone again in Teams or Zoom

**What to tell the user:** "Windows has a built-in audio diagnostic tool that can find and fix common microphone problems automatically. Let's run it now — it checks drivers, settings, and device status all at once."

### Step 5: Check External Microphone Connections and Drivers
1. For USB microphones or headsets:
   - Unplug the USB cable and plug it into a different USB port
   - Avoid USB hubs — connect directly to the computer
   - Wait for Windows to detect the device (you should hear a connection sound)
2. For Bluetooth headsets:
   - Ensure Bluetooth is ON: Settings > Bluetooth & devices
   - Remove the headset (click "..." > Remove device) and pair it again
   - Check the headset battery level
3. Check Device Manager for driver issues:
   - Press Win + X > Device Manager
   - Expand "Audio inputs and outputs"
   - Look for your microphone — if it has a yellow triangle, there is a driver problem
   - Right-click the microphone > "Update driver" > "Search automatically for drivers"
4. If the device does not appear at all, click "Scan for hardware changes" in Device Manager

**What to tell the user:** "If you're using an external microphone, the connection might be loose or the driver might need updating. USB ports can sometimes stop recognizing devices. Let's try a different port and check for driver updates."

### Step 6: Reset Teams or Zoom Audio Settings
1. If the microphone works elsewhere but still fails in the app, the app's audio profile may be corrupted
2. Microsoft Teams:
   - Completely exit Teams (right-click the Teams icon in the system tray > Quit)
   - Press Win + R, type %appdata%\Microsoft\Teams, and press Enter
   - Delete the "settings.json" file
   - Restart Teams — it will create a fresh settings file
3. Zoom:
   - Completely exit Zoom (right-click Zoom icon in system tray > Exit)
   - Press Win + R, type %appdata%\Zoom, and press Enter
   - Delete the "settings.ini" file
   - Restart Zoom — it will create a fresh settings file
4. After resetting, go back into audio settings and select your microphone again
5. Run a test call to verify

**What to tell the user:** "The app's settings file may have gotten corrupted. We're going to delete the old settings file, which forces the app to create a fresh one. You'll need to re-select your microphone afterward, but all your other settings and chats are safe."

---

## Alternative Solutions

If the above steps do not resolve the issue, also try:

- Using the web browser version of Teams or Zoom as a temporary workaround
- Plugging in a different microphone or headset to determine if the original device is faulty
- Checking if another application has exclusive control of the microphone (close all other apps that might use audio)
- Updating or reinstalling the audio driver from your computer manufacturer's website

---

## Prevention Tips

- Before important meetings, use the "Make a test call" feature in Teams or "Test Mic" in Zoom
- Keep your audio drivers updated through Windows Update
- Label USB ports or mark your preferred microphone with a sticker for quick identification
- Close other applications that use audio (music players, voice chat, games) before joining meetings
- Keep Bluetooth headsets charged — low battery causes audio dropouts

---

## Root Cause

Common causes of microphone issues in Teams or Zoom, in order of likelihood:

- Wrong microphone selected in the app's audio settings (most common)
- User is muted in the meeting and unaware
- Windows privacy settings blocking microphone access for the app
- App permissions not granted for microphone use
- Physical mute button enabled on headset or external microphone
- USB or Bluetooth connection issue with external microphone
- Audio driver outdated or corrupted after a Windows Update
- Conflicting application using the microphone exclusively

---

## Escalation Decision Matrix

| Condition | Action |
|-----------|--------|
| All 6 steps completed, issue persists | Escalate to Tier 2 |
| Microphone not detected in Windows at all | Escalate — possible hardware failure |
| Audio driver update does not resolve issue | Escalate — may need manufacturer-specific driver |
| Issue affects multiple users in the same meeting | Escalate — possible Teams/Zoom service issue |
| Microphone detected but produces no sound on any app | Escalate — possible hardware defect |
| Bluetooth microphone repeatedly disconnects | Escalate — Bluetooth stack or hardware issue |
| App reset and driver update resolves the issue | Do not escalate — document solution |

---

## Related Articles

- [Fix Microphone & Camera Issues — Quick Check](../Tier-0-Self-Service/fix-mic-camera-issues.md) — Tier 0: Self-service audio/video check
- [Audio Driver Conflict & Device Enumeration Diagnostics](../Tier-2-Technical-Support/audio-driver-conflict.md) — Tier 2: Advanced audio diagnostics
- [Network QoS & Real-Time Traffic Packet Loss Analysis](../Tier-3-Expert-Engineering/network-qos-packet-loss.md) — Tier 3: Expert audio network analysis

> **Note:** The following related articles are planned for future creation within their respective tier folders:
> - [Fix Microphone & Camera Issues — Quick Check](../Tier-0-Self-Service/fix-mic-camera-issues.md)
> - [Audio Driver Conflict & Device Enumeration Diagnostics](../Tier-2-Technical-Support/audio-driver-conflict.md)
> - [Network QoS & Real-Time Traffic Packet Loss Analysis](../Tier-3-Expert-Engineering/network-qos-packet-loss.md)

---

## FAQ

**Q: Why can people hear me in Zoom but not in Teams?**
**A:** Each app has its own audio settings and permissions. Check that the correct microphone is selected in Teams settings, and that Windows privacy settings allow Teams to use the microphone. The app may also be muted separately from your system mute.

**Q: Why does my microphone sound robotic or cutting out?**
**A:** This is usually a network issue, not a microphone issue. Poor internet connection causes audio packet loss. Try switching from Wi-Fi to a wired connection, or move closer to your router. Closing other apps that use bandwidth (streaming, downloads) also helps.

**Q: Can I use my phone as a microphone for my computer?**
**A:** Yes, but it requires third-party apps and is not officially supported by Teams or Zoom. It is better to use a proper headset or microphone. If you are in an emergency, you can join the meeting from your phone while still viewing content on your computer.

---

## Teams and Zoom Audio Settings Quick Reference

| Setting | Teams Path | Zoom Path |
|---------|------------|-----------|
| Select Microphone | Settings > Devices > Audio devices | Settings > Audio > Microphone |
| Test Microphone | Make a test call button | Test Mic button |
| Reset Settings File | %appdata%\Microsoft\Teams\settings.json | %appdata%\Zoom\settings.ini |
| Desktop App Permissions | Windows Settings > Privacy > Microphone | Windows Settings > Privacy > Microphone |

---

## Was this article helpful?

If this article helped resolve your issue, great. If something was unclear, missing, or did not work, please open a GitHub Issue describing the problem so we can improve it.

Suggest improvements at: https://github.com/EzioLockhart/Complete-IT-Support-Knowledge-Base-Tier-0-to-Tier-3/issues

---

## References

- CompTIA A+ Troubleshooting Methodology: Identify the problem, Establish a theory, Test the theory, Establish a plan of action, Verify functionality, Document findings
- ITIL Incident Management best practices: Prioritize based on impact and urgency; audio issues prevent meeting participation
- Microsoft Teams Help: Troubleshoot audio and video issues
- Zoom Help Center: Testing and troubleshooting microphone issues

---

*Tier: Tier 1 (Help Desk) | Difficulty: L1 (Basic) | Estimated Resolution Time: 10-15 minutes | Required Access Level: User | Severity: P1 (Single User Critical)*

---

For internal use. Follow your organization's meeting and communication policies.
