# Configuring the WiFi on Bebops

> Configure the network and IP on Bebop 2 drones and make changes persistent by adding them to the boot sequence.

---

## Step 1: Clone GitHub Repository and Edit `shortpress_3.sh`

---

### 1. Clone the repository:

```bash
git clone https://github.com/tnaegeli/multiple_bebops.git
```

---

### 2. Navigate to the cloned directory:

```bash
cd multiple_bebops
```

---

### 3. Edit `shortpress_3.sh` to set SSID, password, and static IP:

- Open `shortpress_3.sh` in a text editor.
- Modify the following variables:

  ```
  SSID: NCRLab
  PW: jollypiano265
  IP: 192.168.1.1XX
  ```

- The IP must be in the correct range—refer to the **Autonomy Park NCR Lab IP Reservations** document on Google Drive.
- After configuring, **add the new IP** to the reservations list.

---

## Step 2: Connect to the Bebop Using Android Debug Bridge (ADB)

---

### 1. Install `adb` (if not installed):

```bash
sudo apt-get install android-tools-adb
```

---

### 2. Connect `adb` to the Bebop:

- Connect the Bebop to your computer via USB.
- Power on the Bebop and wait for the LED to remain solid.
- Press the power button **four times** until you hear the beeping sound.
- Then run:

```bash
adb connect 192.168.43.1:9050
```

- A successful message should read:  
  `connected to 192.168.43.1:9050`

---

## Step 3: Run Script and Add to Boot

---

### 1. Run the file copy script:

```bash
./copy_files.sh
```

---

### 2. Open a shell on the Bebop:

```bash
adb shell
```

---

### 3. Edit the boot file:

```bash
nano /etc/init.d/rcS
```

---

### 4. Add this line to the end of the `rcS` file:

```bash
./bin/onoffbutton/shortpress_3.sh
```

---

### 5. Disconnect and reboot the Bebop:

```bash
adb disconnect
```

Unplug the USB and restart the drone.

---

## Notes

- Ensure **all Bebop IPs are unique** and in the reserved range.
- If `adb` isn't working, confirm the drone is powered on and connected via USB.
- If you encounter file system permission issues, remount the filesystem as writable:

```bash
adb shell mount -o remount,rw /
```
