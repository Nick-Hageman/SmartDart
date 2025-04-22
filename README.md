#  ![transparentLogoSmartDart](https://github.com/user-attachments/assets/3fbc8e25-96fd-48b7-b027-0a79216512cf)

A computer vision-based steel-tipped dartboard detection system, powered by a fine-tuned DeepDarts model. Our setup includes a Raspberry Pi with camera integration, a GUI display, and a companion iOS app for live tracking and scoring.

---

## 🎯 Overview

This project combines embedded systems and computer vision to track and score steel-tipped darts in real-time. Our setup includes:

- A **Raspberry Pi** with a camera to capture dart throws.
- A **GUI display** connected to the Pi for real-time feedback.
- A fine-tuned version of the **DeepDarts** model for dart detection and scoring.
- An **iOS companion app** for user interaction, score display, and game management.

---

## 🧠 Tech Stack

| Component         | Technology                 |
|------------------|----------------------------|
| Embedded System  | Raspberry Pi (Python)      |
| Computer Vision  | Fine-tuned DeepDarts model |
| Mobile App       | Swift / SwiftUI (iOS)      |
| GUI              | PyQt / Tkinter / Custom GUI|
| Communication    | WiFi / HTTP / Bluetooth    |

---

## 🛠️ Installation

### 📦 Requirements

- Raspberry Pi 4 or later
- Pi-compatible camera module
- Python 3.8+

### ⚙️ Setup

#### On Raspberry Pi:

```bash
git clone https://github.com/Nick-Hageman/SmartDart-GUI.git
pip install -r requirements.txt
python firebaseGUI.py
