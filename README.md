# Hand-Cursor-Controller
GestureGlide: Hand Tracking System Controller
Developed by: Shivendra | B.Tech ITCY, DTU

📌 Overview

This project is a real-time system controller that uses Computer Vision to replace a physical mouse and keyboard shortcuts. It uses MediaPipe for hand landmark detection and a custom-trained PyTorch Neural Network to classify specific gestures.

🛠️ How it Works

Landmark Extraction: I used MediaPipe to extract 21 hand landmarks (63 total X,Y,Z coordinates).

Wrist Normalization: To make the model work regardless of where the hand is on the screen, I subtracted the wrist coordinates (Landmark 0) from all other points.

Neural Network: I built a 3-layer MLP (Multi-Layer Perceptron) in PyTorch to classify the processed coordinates into 7 different classes.

Temporal Smoothing: I used a deque buffer to average the last 5 frames. This prevents the cursor from jittering or clicking accidentally.

🎮 Gesture Mappings

Gesture	System Action
Up / Palm	Move Cursor: Tracks the index finger tip.
Fist	Left Click: Triggers a mouse click.
Down	Scroll: Automatically scrolls down the page.
Thumbs_up	Volume Up: Increases system volume.
Thumbs_down	Volume Down: Decreases system volume.
Three Fingers	Tab Slide: Swipe left/right to switch workspaces (Mac).
None / Peace	Idle: The system does nothing.
📂 Project Structure

collect_data.ipynb: Script to record hand gestures and save them to gestures.csv.

train_model.ipynb: PyTorch training script that outputs gesture_model.pth.

main.ipynb: The execution script that runs the webcam and controls the OS.

gestures.csv: The dataset (approx. 200 frames per gesture).

gesture_model.pth: The trained weights for the Neural Network.

⚙️ Setup & Installation

Install dependencies:

Bash
pip install opencv-python mediapipe torch pyautogui pandas scikit-learn
Permissions: On macOS, ensure you grant Accessibility and Input Monitoring permissions to your IDE (VS Code/Terminal).

Run: Open main.ipynb and run the cells. Press 'q' to stop the webcam.

💡 Challenges Solved

Coordinate Scaling: Fixed the issue where the 640x480 webcam didn't reach the corners of the screen by using np.interp with a 15% margin.

State Management: Managed a "cooldown" for clicking and sliding so the system doesn't trigger multiple times in a single second.

Indentation Errors: Spent a lot of time debugging Python indentation issues within the OpenCV loop.