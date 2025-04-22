# ![transparentLogoSmartDart-White](https://github.com/user-attachments/assets/45f24b3b-3012-4d5a-9095-dfa60ff5bd01)

A computer vision-based steel-tipped dartboard detection system, powered by a fine-tuned DeepDarts model. Our setup includes a Raspberry Pi with camera integration, a GUI display, and a companion iOS app for live tracking and scoring.

---

## 🎯 Overview

This project combines embedded systems and computer vision to track and score steel-tipped darts in real-time. Our setup includes:

- A **Raspberry Pi** with a camera to capture dart throws.
- A **GUI display** connected to the Pi for real-time feedback.
- A fine-tuned version of the **DeepDarts** model for dart detection and scoring.
- An **iOS companion app** for user interaction, score display, and game management.

---
## 🎯 Model Fine Tuning
We based our dart detection computer vision off of [DeepDarts](https://arxiv.org/abs/2105.09880), the first deep learning-based automatic scoring system for steel-tip darts. It predicts dart scores from a single image taken from any camera angle.

![shortened](https://github.com/user-attachments/assets/0e79066a-056f-4ae3-8850-f6e9d3ec1573)

We manually placed and annotated over 3,000 darts in various locations over the board to fine tune our model. We also utilized data augmented such as rotations, jitter, and warping in the training process.

---

## 🧠 Tech Stack

| Component         | Technology                 |
|------------------|----------------------------|
| Embedded System  | Raspberry Pi (Python)      |
| Computer Vision  | Fine-tuned DeepDarts model |
| Mobile App       | Swift / SwiftUI (iOS)      |
| GUI              | Tkinter |
| Communication    | WiFi |

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
