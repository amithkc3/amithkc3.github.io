---
title: Ambilight TV
date: 2025-03-22 00:00:00 +0530
categories: [Projects, Computer vision]
image: assets/2025-04-22-Ambilight_TV/Ambilight-TV-thumbnail.png
tags: [project, OpenCV, Raspberry-pi, ESP8266, github]     
---

## Summary

Transform your TV setup into an immersive Ambilight experience! This project captures the edges of your screen using Python, processes the colors with OpenCV, and sends the data over UDP to a NodeMCU ESP8266 that powers a NeoPixel strip behind your TV. With minimal hardware and open-source code, you’ll enjoy dynamic backlighting that matches your content in real time.

## Motivation

Bias lighting improves contrast and reduces eye strain by illuminating the area around your display. Commercial Ambilight solutions can be expensive or proprietary—this DIY approach gives you full control using familiar components and Python.

## How It Works

1. **Capture**: A Python script continuous screen grabs with `mss`.
2. **Extract & Filter**: Crop the top, bottom, left, and right edges; convert BGR to HSV; apply brightness and saturation thresholds; smooth over time.
3. **Transmit**: Flatten the processed colors into a single data string and send it over UDP to a microcontroller (ESP8266) connected to a led strip and attach behind the display.
4. **Render**: ESP8266 parses the incoming string and updates each LED before calling `strip.show()`.

<!-- ## Demo Video

<!-- Placeholder: Embed your YouTube demo here -->
<!-- [![Watch the Ambilight Demo](assets/demo-thumbnail.png)](https://youtu.be/VIDEO_ID) -->

## Implementation Details

**Project Structure**:

```bash
ambilight_tv/
├── ambilight_main.py              # Python capture and UDP sender
├── ambilight_v1_arduino_wifi.cpp  # NodeMCU ESP8266 UDP receiver sketch
├── requirements.txt               # mss, opencv-python, numpy, etc.
└── README.md                      # This documentation
```

**Prerequisites**:

```bash
pip install -r requirements.txt
```

**Running the Python Service**:

```bash
python ambilight_main.py
```

**Deploying to ESP8266**:

1. Open the Arduino IDE and select **NodeMCU ESP8266** as the board.
2. Install and include the **Adafruit_NeoPixel** library.
3. Connect your NodeMCU to the LED strip mounted behind the TV.
4. Load `ambilight_v1_arduino_wifi.cpp`, then compile and upload to the board.

## Results & Evaluation

- **Real-Time Ambiance**: LEDs update seamlessly with on-screen content.
- **Low Latency**: UDP and light processing yield minimal lag—perfect for movies and gaming.

## Future Enhancements

- **Multi-Monitor Support**: Capture and map colors from multiple displays.
- **Adaptive Brightness**: Dynamically adjust LED brightness to match room lighting.
- **Data Compression**: Optimize the color data format for faster updates.
- **Alternate Hardware**: Port the receiver sketch to ESP32 or Raspberry Pi Pico.

---

**Links**

- 💻 [GitHub Repository](https://github.com/amithkc3/ambilight_tv)
- 🐍 [mss on PyPI](https://pypi.org/project/mss/)
- ⚙️ [opencv-python on PyPI](https://pypi.org/project/opencv-python/)
- 📖 [Bias Lighting (Ambilight) – Wikipedia](https://en.wikipedia.org/wiki/Bias_lighting)
