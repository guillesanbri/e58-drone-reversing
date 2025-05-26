# e58-drone-reversing

This project decodes the live video stream from an **E58 drone** over WiFi by reverse engineering its UDP protocol.

> [!NOTE]
> More info about this project at: [guillesanbri.com/drone-video](https://guillesanbri.com/drone-video)

# Main findings
- **Start Command**: The video stream is triggered by sending a specific UDP payload `0xEF 0x00 0x04 0x00` to port 8800.
- **Packet Structure**
  - Each frame is split across multiple UDP packets.
  - Each packet has a **56-byte custom header**, followed by the actual image fragment.
  - **Byte 3** in the header marks the last packet of a frame.
  - **Byte 32** indicates the fragment index within a frame.
  - **Bytes 16-17** increment with each frame, acting as frame number.
- **JPEG Decoding**
  - The image data lacks standard JPEG headers.
  - The headers are added manually (SOI, SOF, DQT, SOS, EOI).
- **Frame Requests**
  - After the initial "start video" request, the drone expects custom "next frame" requests to continue streaming at higher frame rates (~20 FPS).
  - These request packets must include an incrementing frame index in multiple locations.

# Setting Up

1. Install [uv](https://github.com/astral-sh/uv) if you don't have it:
```bash
curl -Ls https://astral.sh/uv/install.sh | sh
```

2. Clone the repo
```bash
git clone https://github.com/guillesanbri/e58-drone-reversing.git
cd e58-drone-reversing
```

3. Create the virtual environment and install dependencies:

```bash
uv venv
uv pip install .
```

4. Run the script:
```bash
uv run main.py
```
