# 🎛️ Volume Control Using Webcam

A computer vision project that uses hand gestures to control system volume in real-time. Built using Python, OpenCV, and MediaPipe, this project leverages hand-tracking to detect the distance between the thumb and index finger, translating it into volume levels.

## 📽️ Demo

https://github.com/Ashishverma66/Volume_Control_using_webcam/assets/... *(Add a demo video or GIF here if available)*

## ✨ Features

- Real-time hand tracking with MediaPipe
- Dynamic volume adjustment using finger distance
- Smooth volume transition with interpolation
- Visual feedback via on-screen volume bar

## 🧰 Technologies Used

- Python
- OpenCV
- MediaPipe
- Numpy
- Pycaw (Python Core Audio Windows Library)

## 🖥️ How It Works

1. Webcam feed is captured using OpenCV.
2. MediaPipe detects hand landmarks.
3. Distance between thumb and index finger is calculated.
4. The distance is mapped to a volume range using `np.interp`.
5. Pycaw sets the system volume based on the calculated distance.

## 📁 Project Structure


