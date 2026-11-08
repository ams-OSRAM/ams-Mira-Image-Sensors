# Mira Image Sensors: Camera Boards

**[← Back to Main Page](/README.md)**

---

## 🎯 Overview

ams OSRAM offers **open-source reference designs** for Mira image sensors. You can:

- 🏭 **Manufacture your own boards** using the provided design files
- 🛒 **Purchase ready-made boards** from authorized distributors

### Available Distributors

- [Digi-Key](https://www.digikey.com)
- [Mouser Electronics](https://www.mouser.com)
- [Farnell](https://www.farnell.com)
- [Rutronik](https://www.rutronik.com)

---

## 📷 Camera Board Models

<table>
  <tr>
    <th>Mira050</th>
    <th>Mira220</th>
    <th>Mira016</th>
  </tr>
  <tr>
    <td align="center">
      <img src="https://look.ams-osram.com/transform/2e384aa6-f0bb-469e-bb11-84fa3b1feff5/Mira050-IM001268-1-00" width="200" alt="Mira050 Camera Board" />
    </td>
    <td align="center">
      <img src="https://look.ams-osram.com/transform/500ef14d-31c2-4142-881d-7061b992c443/Mira220-IM001270-1-00" width="200" alt="Mira220 Camera Board" />
    </td>
    <td align="center">
      <img src="https://look.ams-osram.com/transform/d6a33393-efd2-48f5-9375-f44636e4a3fe/Mira016-IM001269-1-00" width="200" alt="Mira016 Camera Board" />
    </td>
  </tr>
</table>

---

## ✨ Key Features

| Feature | Description |
|---------|-------------|
| **Image Sensor** | Mira series CMOS image sensor |
| **Integrated Components** | On-chip oscillator, LDO, and sequencer |
| **GPIO Access** | Available for trigger or illumination synchronization |
| **Open Source** | Hardware and software designs available |
| **Raspberry Pi Compatible** | Works with all Raspberry Pi models with CSI port |
| **Commercial Availability** | Purchase through authorized distributors |

---

## 📐 Technical Documentation

### Schematics

| Model | Schematic PDF |
|-------|---------------|
| **Mira220** | [Download Schematics](Mira220/Output/PDF/Schematic%20Prints.PDF) |
| **Mira050** | [Download Schematics](Mira050/Output/PDF/Schematic%20Print/Schematic%20Prints.PDF) |
| **Mira016** | [Download Schematics](Mira016/Output/PDF/Schematic%20Print/MIRA016%20CSP%20Reference%20Design.PDF) |

### Design Files

Each board folder contains the Altium project, a bill of materials, Gerber/manufacturing files and a 3D STEP model.

| Model | Altium Project | BOM | Gerber / MFG | STEP |
|-------|----------------|-----|--------------|------|
| **Mira220** | [Mira220/](Mira220/) | [BOM](Mira220/Output/BOM/BOM-MIRA220CSP-ReferenceDesign.ods) | [MFG.7z](Mira220/Output/MFG/MFG.7z) | [STEP](Mira220/Output/ExportSTEP/MIRA220CSP.7z) |
| **Mira050** | [Mira050/](Mira050/) | [BOM](Mira050/Output/BOM/Bill%20of%20Materials-MIRA050CSP-ReferenceDesign.xlsx) | [MFG.7z](Mira050/Output/MFG/MFG.7z) | [STEP](Mira050/Output/ExportSTEP/MIRA050CSP.7z) |
| **Mira016** | [Mira016/](Mira016/) | [BOM](Mira016/Output/BOM/Bill%20of%20Materials-MIRA016-CSP.xlsx) | [MFG.7z](Mira016/Output/MFG/MFG.7z) | [STEP](Mira016/Output/ExportSTEP/MIRA016-CSP.7z) |

---

## 🔧 Required Accessories

To complete your camera setup, you'll need the following components:

### Optical Components

| Component | Specifications | Link |
|-----------|---------------|------|
| **M12 Lens** | 4mm focal length | [Lensation B3M4016](https://www.lensation.de/product/B3M4016/) |
| **Lens Holder** | M12 mount compatible | [Lensation SH02M13V3](https://www.lensation.de/product/sh02m13v3/) |

### Mounting Hardware

| Component | Specifications | Link |
|-----------|---------------|------|
| **Mounting Screws** | DIN 7981 Form CH<br>Stainless Steel A2<br>2.2mm diameter | [Online-Schrauben Shop](https://online-schrauben.de/shop/Schrauben/Blechschrauben/DIN-7981-Form-CH-Linsenkopf-Blechschrauben-mit-Phillips-Kreuzschlitz-und-Spitze-aehnl.-ISO-7049/Edelstahl-Rostfrei-A2/2,2-mm-Schraubendurchmesser) |

### Connection Cable

| Component | Description | Link |
|-----------|-------------|------|
| **Camera Cable** | Raspberry Pi CSI cable, 15-pin to 15-pin (Pi 3, Pi 4) | [Adafruit 1648 @ Mouser](https://www.mouser.at/ProductDetail/Adafruit/1648?qs=GURawfaeGuAYPzNMiqAbyQ%3D%3D) |
| **Camera Cable (Pi 5, Zero 2 W)** | 22-pin to 15-pin cable for the smaller camera connector | [Raspberry Pi camera cables](https://www.raspberrypi.com/products/camera-cable/) |

---

## 🛠️ Assembly Guide

### Step 1: Prepare Components
1. Gather all required accessories listed above
2. Ensure you have a compatible Raspberry Pi board
3. Verify the camera cable fits your Pi: Pi 5 and Zero 2 W need a 22-pin to 15-pin cable

### Step 2: Mount the Lens
1. Attach the lens holder to the camera board using the mounting screws
2. Carefully thread the M12 lens into the holder
3. Focus can be adjusted by rotating the lens after initial installation

### Step 3: Connect to Raspberry Pi
1. Power off your Raspberry Pi
2. Connect the camera cable to the CSI port on both the camera board and Raspberry Pi
3. Ensure the cable is fully seated and the connector locks are engaged

### Step 4: Software Setup
Refer to the [Software Guide](/software/README.md) for driver and libcamera installation instructions.

---

## 📦 Ordering Information

### Pre-Built Boards

Contact authorized distributors for availability and pricing:

- **Digi-Key**: Search for "ams OSRAM Mira"
- **Mouser Electronics**: Search part numbers for specific models
- **Farnell**: Check regional availability
- **Rutronik**: Contact for volume pricing

### Custom Manufacturing

If you prefer to manufacture your own boards:

1. Download the design files from the [tables above](#-technical-documentation)
2. Send the Gerber/manufacturing files to a PCB manufacturer of your choice
3. Source components based on the Bill of Materials (BOM)

---

## 🆘 Support

### Getting Help

For questions, issues, or suggestions:

- 📝 **Open an issue** in the [GitHub issue tracker](https://github.com/ams-OSRAM/ams-Mira-Image-Sensors/issues)
- 📧 **Contact [ams OSRAM support](https://ams-osram.com/support)**

### Common Issues

| Issue | Solution |
|-------|----------|
| Camera not detected | Check the cable connection and the `dtoverlay=` line in `/boot/firmware/config.txt` |
| Poor image quality | Verify lens is properly focused and clean |

---

## 🔗 Related Resources

- [Software Setup Guide](/software/README.md)
- [ams OSRAM GitHub Organization](https://github.com/ams-OSRAM)
- [Raspberry Pi Camera Documentation](https://www.raspberrypi.com/documentation/accessories/camera.html)
- [MIPI CSI-2 Specification](https://www.mipi.org/specifications/csi-2)

---

*Last updated: November 2026*
