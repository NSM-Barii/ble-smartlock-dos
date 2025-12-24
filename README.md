# BLE Smart Lock Denial-of-Service (DoS) Vulnerability

> An unauthenticated Bluetooth Low Energy (BLE) connection flood can reliably prevent legitimate users from unlocking the device by interrupting keypad input and forcing repeated lockout states.

---

## 📌 Summary

This repository documents a **Denial-of-Service (DoS)** vulnerability affecting a commercial BLE smart padlock  
([Amazon Product](https://www.amazon.com/dp/B0F9L1M4XG)).

The device exposes a **static BLE MAC address (no RPA)** and accepts unauthenticated connection attempts. By repeatedly initiating BLE connections in a loop, an attacker can interfere with the lock’s keypad authentication flow, preventing users from completing PIN entry.

This behavior is **not caused by incorrect password attempts** — the user is denied sufficient time to enter the PIN before the device forcibly enters a lockout state.

---

## 🔥 Impact

- ❌ Prevents legitimate users from unlocking the device
- ⛔ Keypad becomes unresponsive mid‑input
- 🔁 Forced lockout occurs every **10–15 seconds**
- 🧠 Lockout is triggered **by BLE interference**, not invalid PIN attempts
- 🔓 Works on default and custom configurations
- 📡 Target uses a **static MAC address**, allowing persistent targeting
- 🚫 No pairing or authentication required

As long as the attack is sustained, the device remains effectively unusable.

---

## 🧪 Attack Prerequisites

- BLE‑capable system (Linux or macOS recommended)
- Python 3.x
- `bleak` library
- Target device MAC address  
  (broadcast after pressing the physical pairing button on the lock)

---

## 🚀 Proof of Concept

### Install Dependencies
```bash
pip install bleak
