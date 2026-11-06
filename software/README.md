# Mira Image Sensors: Software Guide

### [← Back to Main Page](/README.md)

---

## Overview

Mira image sensors feature a standard **MIPI CSI-2 camera interface**, ensuring broad compatibility with various platforms:

- **Single Board Computers**: Raspberry Pi, NXP i.MX
- **Microprocessors**: Qualcomm, STM32MP
- **Microcontrollers**: ESP32-P4

This guide focuses on Raspberry Pi setup, though the V4L2 Linux driver is compatible with most Linux devices.

---

## Requirements

To operate a Mira camera board with your Raspberry Pi, you'll need:

1. **Mira V4L2 Driver** - Kernel module for hardware communication
2. **Libcamera Framework** - ISP (Image Signal Processor) framework with Mira support

---

## Setup Instructions

### Step 1: Prepare Your SD Card

1. Download the latest [Raspberry Pi OS 64-bit](https://www.raspberrypi.com/software/operating-systems/)
2. Use [Raspberry Pi Imager](https://www.raspberrypi.com/software/) to flash your SD card (**recommended**)
   - Configure OS settings during flashing:
     - User credentials
     - WiFi network
     - SSH access
     - USB gadget mode (if needed)
3. Insert the SD card and boot your Raspberry Pi

---

### Step 2: Install the Kernel Module and Device Tree

Install the tools and the kernel headers for the running kernel:

```bash
sudo apt update
sudo apt install -y git linux-headers-$(uname -r)
```

Then choose your sensor model:

- **Mira220**: [Linux Driver & Installation Guide](https://github.com/ams-OSRAM/mira220_v4l2_driver)
- **Mira050 / Mira016**: [Linux Driver & Installation Guide](https://github.com/ams-OSRAM/mira050_016_v4l2_driver) (one driver for both sensors)

Clone the driver repository and follow the steps in its README, for example:

```bash
cd ~
git clone https://github.com/ams-OSRAM/mira050_016_v4l2_driver.git
cd mira050_016_v4l2_driver
make
```

> 💡 **Mira220**: Raspberry Pi OS already ships a Mira220 driver (kernel 6.12 and later), so `dtoverlay=mira220` works without building anything. Build the driver from [mira220_v4l2_driver](https://github.com/ams-OSRAM/mira220_v4l2_driver) only if you need a newer version than the one in your kernel.


---

### Step 3: Build Libcamera

Libcamera is the ISP framework that works alongside the V4L2 driver to process camera data.

#### Install Libcam Dependencies

```bash
# Remove existing camera packages
sudo apt remove --purge libcamera-dev

# Install build dependencies
sudo apt install -y libboost-dev libgnutls28-dev openssl libtiff5-dev pybind11-dev
sudo apt install -y qtbase5-dev libqt5core5a libqt5gui5 libqt5widgets5
sudo apt install -y meson cmake python3-yaml python3-ply
sudo apt install -y libglib2.0-dev libgstreamer-plugins-base1.0-dev
```

#### Clone and Build Libcamera

```bash
# Clone the Mira-enabled libcamera fork
cd ~
git clone https://github.com/ams-OSRAM/libcamera.git
cd libcamera

# Configure the build
meson setup build --buildtype=release \
  -Dpipelines=rpi/vc4,rpi/pisp \
  -Dipas=rpi/vc4,rpi/pisp \
  -Dv4l2=enabled \
  -Dgstreamer=enabled \
  -Dtest=false \
  -Dlc-compliance=disabled \
  -Dcam=disabled \
  -Dqcam=disabled \
  -Ddocumentation=disabled \
  -Dpycamera=enabled

# Compile and install
ninja -C build
sudo ninja -C build install
sudo ldconfig
```

---

### Step 4: Rebuild rpicam-apps

The `rpicam-apps` that ship with Raspberry Pi OS are linked against the stock libcamera. Rebuild them so they use the Mira-enabled libcamera installed above.

```bash
# Install build dependencies
sudo apt install -y libboost-program-options-dev libdrm-dev libexif-dev
sudo apt install -y libjpeg-dev libpng-dev libepoxy-dev ninja-build

# Clone, build and install
cd ~
git clone https://github.com/raspberrypi/rpicam-apps.git
cd rpicam-apps
meson setup build -Denable_libav=disabled -Denable_drm=enabled -Denable_egl=enabled   -Denable_qt=enabled -Denable_opencv=disabled -Denable_tflite=disabled -Denable_hailo=disabled
meson compile -C build
sudo meson install -C build
sudo ldconfig
```

---

#### Test Your Setup

```bash
rpicam-hello
```

If successful, you should see a live camera preview on your display.

---

## Optional: Python Bindings (not needed)

To use your Mira camera with Python, install **picamera2** in a virtual environment.

### Setup Virtual Environment

```bash
cd ~
python3 -m venv .venv --system-site-packages
source .venv/bin/activate
```

### Test Python Integration

```python
from picamera2 import Picamera2

picam2 = Picamera2()
picam2.start_preview()
picam2.start()
```

---

## Troubleshooting

### Camera Not Detected

- Verify the ribbon cable is properly seated in both the camera and Raspberry Pi connectors
- Check that `/boot/firmware/config.txt` contains the `dtoverlay=` line for your sensor, then reboot
- List the cameras libcamera sees: `rpicam-hello --list-cameras`
- Confirm the driver loaded correctly: `dmesg | grep mira`

### Build Errors

- Ensure all dependencies are installed
- Try updating your system first: `sudo apt update && sudo apt upgrade`
- Check for adequate disk space: `df -h`

### Python Import Errors

- Ensure the virtual environment has `--system-site-packages` enabled
- Check libcamera installation: `ldconfig -p | grep libcamera`

---

## Additional Resources

- [Raspberry Pi Camera Documentation](https://www.raspberrypi.com/documentation/accessories/camera.html)
- [Libcamera Documentation](https://libcamera.org/docs/)
- [V4L2 Documentation](https://www.kernel.org/doc/html/latest/userspace-api/media/v4l/v4l2.html)

---

## Support

For issues specific to Mira sensors, please visit:
- [ams-OSRAM GitHub Organization](https://github.com/ams-OSRAM)
- The issue tracker of the driver repository for your sensor: [Mira220](https://github.com/ams-OSRAM/mira220_v4l2_driver/issues), [Mira050 / Mira016](https://github.com/ams-OSRAM/mira050_016_v4l2_driver/issues)

---

*Last updated: November 2026*
