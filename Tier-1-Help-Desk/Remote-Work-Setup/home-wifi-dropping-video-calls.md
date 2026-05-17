# Home Wi-Fi Keeps Dropping During Video Calls

- **Category:** Remote Work Setup
- **Tier:** Tier 1 (Help Desk)
- **Version:** 1.0
- **Last Updated:** May 2, 2026
- **Last Reviewed:** May 2, 2026
- **Applies To:** Windows 10 (22H2), Windows 11 (23H2), Home Wi-Fi Networks, All Video Conferencing Applications
- **Difficulty:** L1 (Basic)
- **Estimated Resolution Time:** 10-20 minutes
- **Required Access Level:** User
- **Severity:** P1 (Single User, Critical — Cannot Participate in Video Calls)
- **Keywords:** Wi-Fi, drops, video calls, home network, router, interference, bandwidth, Teams, Zoom, stability
- **Prerequisite Knowledge:** Basic home network understanding, ability to access router settings

---

## Symptoms

- Wi-Fi disconnects specifically during video calls but works otherwise
- Video freezes, audio cuts out, or call drops entirely during meetings
- "Your network connection is unstable" message in Teams or Zoom
- Other household members streaming or gaming when call quality drops
- Wi-Fi signal strength appears strong but performance is poor
- Issue happens consistently at specific times of day
- Router needs frequent rebooting to restore connection

---

## Common Error Codes

| Code | Meaning |
|------|---------|
| ERR_NETWORK_CHANGED | Network connection changed or dropped during call |
| 0x80072746 | Connection was terminated by remote host — timeout during call |
| Event ID 8002 | Wi-Fi adapter reported disconnection from access point |
| ERR_INTERNET_DISCONNECTED | Complete loss of internet during video call session |

---

## Symptom-to-Step Mapping

| If You See This | Skip To |
|-----------------|---------|
| Wi-Fi drops only during video calls | Step 1 |
| Router is far from workspace | Step 2 |
| Multiple devices streaming simultaneously | Step 3 |
| Wi-Fi works in some rooms but not others | Step 4 |
| Router hasn't been restarted in weeks | Step 5 |

---

## Triage Questions

Before starting troubleshooting, ask the user:

1. "How far is your workspace from your Wi-Fi router, and how many walls are between them?"
2. "Are other people in your home using the internet at the same time — streaming video, gaming, or large downloads?"
3. "Do you have the option to connect your computer directly to the router with an Ethernet cable?"
4. "What internet speed plan are you on, and do you know your actual speed?"

---

## Quick Checks (30 seconds)

1. Move closer to your router and see if the video call stabilizes — if yes, distance or interference is the problem
2. Check how many devices are connected to your Wi-Fi — other devices may be consuming bandwidth
3. Run a speed test (speedtest.net or fast.com) during a non-call time and compare to your internet plan
4. Check if your computer can use a wired Ethernet connection instead of Wi-Fi
5. Restart your router and modem — unplug both for 60 seconds, then plug in modem first, wait, then router
6. If you need general tips for home office internet, see: [Optimize Your Home Office Internet — Quick Guide](../Tier-0-Self-Service/optimize-home-office-internet.md)

---

## Step-by-Step Resolution

### Step 1: Prioritize Video Call Traffic (Quality of Service)
1. Video calls need consistent bandwidth, not just high speed
2. Close unnecessary applications during calls:
   - File downloads and cloud sync (OneDrive, Google Drive, Dropbox)
   - Streaming services (Netflix, YouTube, Spotify)
   - Large file uploads or backups
   - Other video conferencing apps running in background
3. Ask other household members to pause heavy internet use during your calls:
   - Streaming 4K video
   - Online gaming
   - Large downloads or torrents
4. In your video conferencing app:
   - Teams: Settings > Devices > turn off "HD" video if available
   - Zoom: Settings > Video > uncheck "Enable HD" and "Touch up my appearance"
5. Turn off your own video when speaking is sufficient — video consumes far more bandwidth than audio

**What to tell the user:** "Video calls need a steady, reliable connection — like a conversation where you need to hear every word. If someone else in your home is streaming a movie or downloading a large file, they're using most of your internet's capacity. Think of it like a water pipe — if someone else is taking a shower, your water pressure drops. Let's make sure your video call gets priority."

### Step 2: Move Closer to the Router or Reduce Interference
1. Wi-Fi signal weakens with distance and through obstacles
2. Each wall, floor, and large piece of furniture reduces signal strength
3. Ideal placement: computer and router in the same room, with line of sight
4. If moving the router or workspace is not possible:
   - Keep the router elevated (on a shelf, not on the floor)
   - Keep the router away from metal objects, mirrors, fish tanks, and microwaves
   - Avoid placing the router behind TVs or in cabinets
5. Common sources of Wi-Fi interference:
   - Microwave ovens (when running)
   - Cordless phones (especially older 2.4 GHz models)
   - Baby monitors
   - Bluetooth devices in close proximity
   - Neighboring Wi-Fi networks (especially in apartments)
6. Try switching your computer's Wi-Fi between 2.4 GHz and 5 GHz:
   - 5 GHz is faster but has shorter range — best when close to router
   - 2.4 GHz has longer range but more interference — best when far from router

**What to tell the user:** "Wi-Fi is like a conversation in a noisy room — the farther you are, the harder it is to hear clearly. Walls, floors, and even your microwave can interfere with the signal. Moving closer to your router, even by a few feet, can make a dramatic difference in call quality."

### Step 3: Limit Connected Devices During Calls
1. Each device on your Wi-Fi shares the available bandwidth
2. Log into your router's admin page (usually 192.168.1.1 or 192.168.0.1) to see connected devices
3. Identify devices that may be consuming bandwidth:
   - Smart TVs streaming content
   - Gaming consoles downloading updates
   - Security cameras uploading footage
   - Other computers, tablets, and phones
4. Temporarily disconnect or pause Wi-Fi for non-essential devices during important calls
5. Some routers have a "Device Prioritization" or "QoS" feature:
   - Look for it in your router settings
   - Set your work computer as the highest priority device
6. If your router supports guest networks, put household entertainment devices on the guest network separate from your work devices

**What to tell the user:** "Your home Wi-Fi is shared by every device in your house — phones, tablets, smart TVs, gaming consoles, even your doorbell camera. When several of these are active during your video call, they compete for bandwidth. Let's check how many devices are connected and reduce the competition during your meeting times."

### Step 4: Switch to a Wired Ethernet Connection
1. A wired connection is always more stable than Wi-Fi for video calls
2. If your computer has an Ethernet port:
   - Connect an Ethernet cable directly from your computer to your router
   - Windows should automatically switch from Wi-Fi to wired
   - Disable Wi-Fi to ensure the wired connection is used: Settings > Network & Internet > Wi-Fi > toggle OFF
3. If your computer does not have an Ethernet port (common on thin laptops):
   - Use a USB-to-Ethernet adapter (available for $15-30)
   - Plug the adapter into a USB port, then connect an Ethernet cable to your router
4. If the router is too far for a cable:
   - Consider Powerline adapters — they use your home's electrical wiring to transmit network signals
   - Plug one adapter near your router (connected via Ethernet), and the other near your computer
5. Test your video call on the wired connection — it should be dramatically more stable

**What to tell the user:** "Wi-Fi is convenient but inherently unstable for real-time applications like video calls. A wired Ethernet connection is like having a direct line instead of a walkie-talkie — no interference, no dropouts, no competition. Even a simple USB-to-Ethernet adapter can transform your call quality."

### Step 5: Restart Your Router and Modem Regularly
1. Home routers are small computers that can develop issues over time
2. Restart your router and modem at least once a week:
   - Unplug both the modem and router from power
   - Wait 60 seconds (this clears the router's memory and resets connections)
   - Plug in the modem first — wait for all lights to stabilize (about 2 minutes)
   - Plug in the router — wait for it to fully boot (about 2 minutes)
   - Reconnect your computer and test
3. If your router is more than 3-4 years old:
   - Older routers use outdated Wi-Fi standards (Wi-Fi 4 or older)
   - Newer routers (Wi-Fi 5, Wi-Fi 6) handle multiple devices much better
   - Consider upgrading if your router is old
4. Check if your router firmware needs updating:
   - Log into your router's admin page
   - Look for "Firmware Update" or "Router Update" in settings
   - Follow the manufacturer's instructions to update

**What to tell the user:** "Your router runs 24/7, and like any computer, it can get bogged down over time. Memory leaks, temporary glitches, and overheating can all cause your Wi-Fi to become unstable. A weekly restart clears all of this out and gives your router a fresh start."

### Step 6: Test Your Internet Speed and Stability
1. Your internet plan may not provide enough upload speed for video calls
2. Video call requirements:
   - 1-on-1 video call: 1-2 Mbps upload and download
   - Group video call (5+ people): 3-5 Mbps upload and download
   - HD video in calls: 5-10 Mbps upload
3. Run a speed test:
   - Go to speedtest.net or fast.com
   - Run the test during a non-call time and note the download and upload speeds
   - Run it again during a time when calls typically have problems
   - Compare the two results
4. If your upload speed is consistently below 2 Mbps:
   - Video calls will always struggle regardless of other optimizations
   - Contact your ISP about upgrading your plan
   - Ask specifically about plans with higher upload speeds (many basic plans have fast downloads but very slow uploads)
5. Also test for packet loss and jitter:
   - Go to packetlosstest.com
   - Packet loss above 1-2% will cause audio cutouts and video freezing
   - High jitter (variation in ping) causes robotic audio

**What to tell the user:** "Video calls depend heavily on upload speed — how fast your computer can send your video and audio to others. Many internet plans advertise fast download speeds but have very slow upload speeds. If your upload speed is too low, even the best Wi-Fi setup won't help. Let's measure your actual speeds."

---

## Alternative Solutions

If the above steps do not resolve the issue, also try:

- Using your phone's mobile hotspot as a backup internet connection for critical calls
- Changing your router's Wi-Fi channel to a less congested one (use a Wi-Fi analyzer app to see which channels neighbors are using)
- Upgrading to a mesh Wi-Fi system if you have a large home (e.g., Google Nest Wi-Fi, Eero, TP-Link Deco)
- Asking your ISP if they support a faster upload speed tier or fiber optic service

---

## Prevention Tips

- Restart your router and modem weekly — set a recurring reminder
- Before important meetings, close unnecessary applications and pause cloud sync
- Keep your router in a central, elevated location free from obstructions
- Use a wired Ethernet connection whenever possible for critical calls
- Test your internet speed monthly and compare to your plan — contact your ISP if speeds consistently fall short

---

## Root Cause

Common causes of Wi-Fi drops during video calls, in order of likelihood:

- Insufficient upload bandwidth for video calls (most common — basic internet plans have low upload speeds)
- Distance from router or physical obstacles weakening Wi-Fi signal
- Other devices or household members consuming bandwidth during calls
- Router needing a restart due to memory leaks or long uptime
- Wi-Fi interference from neighboring networks, microwaves, or cordless phones
- Outdated router with old Wi-Fi standards that do not handle multiple devices well
- ISP throttling or network congestion during peak hours

---

## Escalation Decision Matrix

| Condition | Action |
|-----------|--------|
| All 6 steps completed, issue persists | Escalate to Tier 2 |
| Speed tests show upload speeds consistently below 2 Mbps | Escalate — user may need ISP plan upgrade |
| Wi-Fi drops persist even on wired Ethernet connection | Escalate — possible ISP or infrastructure issue |
| Router is more than 5 years old and cannot be replaced by user | Escalate for hardware procurement |
| Issue affects only one specific application | Escalate — possible application configuration issue |
| ISP confirmed outage or degraded service in area | Escalate — requires ISP contact |
| Wi-Fi stabilized after wired connection or router restart | Do not escalate — document solution |

---

## Related Articles

- [Optimize Your Home Office Internet — Quick Guide](../Tier-0-Self-Service/optimize-home-office-internet.md) — Tier 0: Self-service home network tips
- [Home Network Performance & QoS Configuration](../Tier-2-Technical-Support/home-network-qos.md) — Tier 2: Advanced network performance
- [Remote Access Architecture & Always-On VPN Design](../Tier-3-Expert-Engineering/remote-access-architecture.md) — Tier 3: Expert remote access design

> **Note:** The following related articles are planned for future creation within their respective tier folders:
> - [Optimize Your Home Office Internet — Quick Guide](../Tier-0-Self-Service/optimize-home-office-internet.md)
> - [Home Network Performance & QoS Configuration](../Tier-2-Technical-Support/home-network-qos.md)
> - [Remote Access Architecture & Always-On VPN Design](../Tier-3-Expert-Engineering/remote-access-architecture.md)

---

## FAQ

**Q: Why is my Wi-Fi fine for everything except video calls?**
**A:** Video calls are uniquely demanding because they need steady, real-time data flow in both directions simultaneously. Browsing websites or streaming video can buffer (pre-load), masking brief Wi-Fi drops. Video calls cannot buffer — any interruption is immediately noticeable as frozen video or cut audio.

**Q: Is 5 GHz always better than 2.4 GHz for video calls?**
**A:** Not always. 5 GHz is faster and less congested, making it better if you are close to the router. But 5 GHz has shorter range and penetrates walls poorly. If you are in another room, 2.4 GHz may actually be more stable, even if slower. Test both on a call to compare.

**Q: Will a better internet plan fix my video call problems?**
**A:** Only if your current upload speed is too low. Check your upload speed first. If it is below 2-3 Mbps, upgrading your plan will help. If your upload speed is already adequate (5+ Mbps), the problem is more likely your Wi-Fi setup, router age, or network congestion — none of which are fixed by a faster plan.

---

## Video Call Bandwidth Quick Reference

| Call Type | Minimum Download | Minimum Upload |
|-----------|:---------------:|:--------------:|
| Audio only | 50 Kbps | 50 Kbps |
| 1-on-1 video | 1 Mbps | 1 Mbps |
| Group video (5 people) | 3 Mbps | 3 Mbps |
| HD video | 5 Mbps | 5 Mbps |
| Screen sharing | 1 Mbps | 1 Mbps |

---

## Was this article helpful?

If this article helped resolve your issue, great. If something was unclear, missing, or did not work, please open a GitHub Issue describing the problem so we can improve it.

Suggest improvements at: https://github.com/EzioLockhart/Complete-IT-Support-Knowledge-Base-Tier-0-to-Tier-3/issues

---

## References

- CompTIA A+ Troubleshooting Methodology: Identify the problem, Establish a theory, Test the theory, Establish a plan of action, Verify functionality, Document findings
- ITIL Incident Management best practices: Prioritize based on impact and urgency; video call issues prevent remote collaboration
- Microsoft Teams Help: Troubleshoot network connectivity issues
- Zoom Help Center: Network requirements for Zoom

---

*Tier: Tier 1 (Help Desk) | Difficulty: L1 (Basic) | Estimated Resolution Time: 10-20 minutes | Required Access Level: User | Severity: P1 (Single User Critical)*

---

For internal use. Follow your organization's remote work and network policies.
