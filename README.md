# ![transparentLogoSmartDart-White](https://github.com/user-attachments/assets/45f24b3b-3012-4d5a-9095-dfa60ff5bd01)

<img src="https://github.com/user-attachments/assets/caed2095-f7e9-4fd6-9cfc-02acd6904624" width="450"/>

> SmartDart brings automated scoring to traditional steel-tip darts by combining computer vision and machine learning. Using a
Raspberry Pi and a high-resolution camera, the system detects dart locations in real time and updates scores automatically, similar to
modern plastic tip-dart machines. By integrating a deep learning model with mobile app connectivity, SmartDart modernizes the
gameplay experience while preserving the unique feel of steel-tip darts.

---

## 🎯 Overview

This project combines embedded systems and computer vision to track and score steel-tipped darts in real-time. Our setup includes:

- A **Raspberry Pi** with a camera to capture dart throws.
- A **GUI display** connected to the Pi for real-time feedback.
- A fine-tuned version of the **DeepDarts** model for dart detection and scoring.
- An **iOS companion app** for user interaction, score display, and game management.

---
## 🔨 Model Fine Tuning

We based our dart detection computer vision off of [DeepDarts](https://arxiv.org/abs/2105.09880), the first deep learning-based automatic scoring system for steel-tip darts. It predicts dart scores from a single image taken from any camera angle.


![shortened](https://github.com/user-attachments/assets/0e79066a-056f-4ae3-8850-f6e9d3ec1573)

> We manually placed and annotated over 3,000 darts in various locations over the board to fine tune our model. We also utilized data augmented such as rotations, jitter, and warping in the training process.


<img src="https://github.com/user-attachments/assets/725ff100-5b95-48b4-8f1c-4276f4d1f79b" width="300"/>

> A heatmap of the training dataset distribution of where the darts were located. We emphasized training towards the center where it's harder to classify the score due to the smaller area.

![yolo](https://github.com/user-attachments/assets/cdf2bf12-e61c-4303-9edb-44601334e133)

> We fine-tuned a YoloV4-tiny model for dart detection. DeepDarts was a paper which had a similar goal of using a single camera to predict dart coordinates. DeepDarts uses a deep learning-based key point detector that models key points as objects to simultaneously detect and localize dart coordinates and four calibration points. The calibration points are used to transform the dart locations to the dart plane and calibrate the scoring area. Once that is done, the darts are then classified based on their position relative to the center of the dartboard. 

```yaml
train:
  seed: 0
  epochs: 100
  batch_size: 4
  lr: 0.001
  bbox_size: 0.025  # fraction of input size
  loss_type: 'ciou'
  loss_verbose: 0
  verbose: 1
  save_weights_type: 'tf'
  val: true
```
> Used the model config above for our training process.

```yaml
aug:
  overall_prob: 0.8
  flip_lr_prob: 0.5
  flip_ud_prob: 0.5
  rot_prob: 0.5
  rot_step: 36  # degrees
  rot_small_prob: 0.5
  rot_small_max: 2  # degrees
  jitter_prob: 0.5
  jitter_max: 0.02  # fraction of input size
  cutout_prob: 0
  warp_prob: 0.5
  warp_rho: 2
```
> Used the configuration above for data augmentation.

📝 DeepDarts research paper [HERE](https://arxiv.org/pdf/2105.09880)

🙌Thanks to [Mike McGarry](https://www.linkedin.com/in/mikejmcgarry/) for sharing [his approach](https://www.linkedin.com/pulse/applying-artificial-intelligence-automatically-score-darts-mcgarry/) for fine-tuning a model from the DeepDarts paper.


---
## 🥧 GUI
![smartDartSketch](https://github.com/user-attachments/assets/21260dee-2d5d-4307-99dd-1a02d5b15349)
![combined](https://github.com/user-attachments/assets/b942305d-c0ee-4b4f-a0fb-bb11265ba4ff)

> Detected scores are displayed in real time
on a Tkinter-based GUI and synchronized
through Firebase to a companion mobile app. The app allows users to correct
scores, track game history, and monitor Elobased player rankings.

## Companion App
![appCombined](https://github.com/user-attachments/assets/e07cde13-5cf6-4f1c-be73-545be5f4339c)

> Our companion app allows players to modify incorrectly predicted dart scores and track user game history. This app was built with Swift.  The user is able to create an account and track their Elo rating (a competitive rating for user rankings), along with other statistics. This app connects to Firebase for two main purposes: getting user account information and participating in  an on-going game. It can only be connected when the Pi is connected to Wi-Fi. On offline mode, the companion app is not intended to be used.

## Power Distribution
![powerDistribution](https://github.com/user-attachments/assets/ccc61447-259d-436a-9d62-f1d1cb9a91a2)

> We successfully integrated a single plug power distribution systems allowing use to power all of the system’s components via a single 120W power supply with two buck converters. This satisfied our power constraint and resulted in clean cable management. 

## Innovation Challenge
<img src="https://github.com/user-attachments/assets/b0a1b8f0-e9ad-49ac-a94a-4a11d3a100a1" width="300"/>

> Our team was awarded the Best Technology Award at the University of Iowa John Pappajohn Entrepreneurial Center Innovation Challenge, receiving $5,000 in funding to support the development of SmartDart.

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
