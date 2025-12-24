# BLE Smart Lock Denial-of-Service (DoS) Vulnerability

> Unauthenticated BLE spam can reliably prevent users from unlocking the device by interrupting keypad input, causing forced lockouts every 10–15 seconds.

---

## 📌 Summary

This repository documents a **Denial-of-Service (DoS)** vulnerability affecting a commercial BLE smart lock ([Amazon Product](https://www.amazon.com/dp/B0F9L1M4XG)).

The attack floods the device with BLE connection attempts using a **static MAC address**, causing the lock’s keypad to become unresponsive before the user can finish entering their PIN. This results in:

- 1–1.5 second input windows
- **Forced 10–15 second lockouts**
- Lock remains unusable during the attack

> Importantly, this behavior occurs **before** the user can finish inputting any pin — this is **not** caused by invalid password attempts.

---

## 🔥 Impact

- ❌ Users can't unlock the device — keypad becomes unresponsive mid-input
- 🔁 Lockout resets every 10–15 seconds as long as the attack runs
- 🔓 Affects locks with **default or custom configuration**
- 💡 Target MAC address is **static** (no RPA), so attack is persistently viable
- 🚫 No pairing or authentication is required

---

## 🧪 Attack Prerequisites

- BLE adapter - Linux 
- Python 3.x
- `bleak` library (`pip install bleak`)
- MAC address of the device (broadcasted after pressing pairing button on lock)

---

## 🚀 Usage

```bash
python3 poc.py -m <target_mac>