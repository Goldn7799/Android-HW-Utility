# 🛠️ Android-HW-Utility

A curated collection of lightweight Shell scripts designed for rooted Android devices. These utilities allow power users and developers to manipulate system properties, bypass carrier restrictions, and control hardware states directly via terminal.

> ⚠️ **Prerequisites:** A rooted Android device (Magisk, KernelSU, or APatch) with Superuser access and a Terminal emulator (e.g., Termux) or ADB shell.

---

## 📜 Available Scripts

### 1. `renableCore.sh` — CPU Core Recovery Utility
* **Description:** Automatically detects all available CPU cores and forces offline/stuck cores back online. On many Android kernels, thermal throttling or aggressive power management (*hotplugging*) forces cores into an offline state and fails to wake them up. This script safely queries system CPU topology and wakes up dormant cores to restore maximum device performance.
* **Key Features:**
 * Dynamic CPU core count detection to prevent out-of-bounds errors.
 * Preserves master core state (`cpu0`).
 * Post-execution verification to check if cores successfully came online.

#### Usage
```bash
su
chmod +x renableCore.sh
./renableCore.sh
```

---

### 2. `changeTTL.sh` — Tethering TTL Bypasser (IPv4 & IPv6)
* **Description:** Modifies the system's default Time To Live (TTL) and Hop Limit value to **`65`** across all active network interfaces (`wlan0`, `rmnet_data*`, `rndis0`, etc.). Setting the TTL value to 65 ensures that data packets passing through tethered devices (like PC or Smart TV via Mobile Hotspot or USB Tethering) arrive at the carrier gateway with a TTL of 64, appearing as native mobile traffic.
* **Key Features:**
 * Configures both IPv4 (`ip4tables` / `sysctl`) and IPv6 (`ip6tables`) rules.
 * Automatically sets network properties for tethering interfaces.
 * Solves hot-spot throttling and carrier tethering data caps.

#### Usage
```bash
su
chmod +x changeTTL.sh
./changeTTL.sh
```

---

## 🚀 Quick Installation

You can clone this repository directly on your device using Termux or git-enabled terminal:

```bash
git clone https://github.com/your-username/Android-HW-Utility.git
cd Android-HW-Utility
su
```

---

## ⚠️ Disclaimer

These scripts modify low-level hardware and networking properties of your Android system.
* Forcing CPU cores online under high temperatures may increase device heat and battery drain.
* Ensure you understand what each command does before executing.
* The maintainers are not responsible for bricked devices, thermal damage, or carrier policy violations.

---

## 🤝 Contributing

Pull requests, improvements, and new hardware/software utility scripts are always welcome! Feel free to open an issue or submit a PR to help expand the toolkit.
