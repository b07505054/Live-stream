# WebRTC Video Call

A simple peer-to-peer video calling application built with **WebRTC**, **WebSocket**, **HTML**, **CSS**, and **Node.js**. This project allows two users (a Sender and a Joiner) to establish a real-time video call over the web, with video streams displayed in the browser.

## Features
- **Real-Time Video Calling**: Connect two users via WebRTC for peer-to-peer video and audio communication.
- **Display Video**: Local and remote video streams are displayed in the browser with customizable layouts.
- **WebSocket Signaling**: Uses a Node.js WebSocket server to handle signaling (Offer, Answer, and ICE Candidate exchange).
- **Simple UI**: Minimalistic interface with username input and call buttons.
- **Cross-Browser Support**: Works on modern browsers supporting WebRTC (e.g., Chrome, Firefox).

## Demo
1. The Sender starts a call and shares their video stream.
2. The Joiner connects to the call and both users' video streams are displayed in real-time:
   - Local video is shown in a small overlay (top-left corner).
   - Remote video occupies the full screen.

## Prerequisites
- **Node.js** (v14 or higher)
- A modern web browser with WebRTC support (e.g., Chrome, Edge, Firefox)
- A local network or public server for WebSocket communication

## Installation
1. **Clone the Repository**:
   ```bash
   git clone https://github.com/your-username/WebRTC-Video-Call.git
   cd WebRTC-Video-Call
   ```

2. **Install Dependencies**:
   Navigate to the server directory and install the required Node.js package:
   ```bash
   npm install ws
   ```

## Usage
1. **Start the WebSocket Server**:
   ```bash
   node server.js
   ```
   - The server will listen on port `3000`. Ensure the IP address in `roomer.js` and `joiner.js` (`ws://192.168.0.118:3000`) matches your server's IP.

2. **Open Sender Page**:
   - Open `sender.html` in a browser.
   - Enter a username, click "Send", then click "Start Call".
   - Your local video will appear in the top-left corner.

3. **Open Joiner Page**:
   - Open `joiner.html` in another browser window or device.
   - Enter the same username as the Sender, then click "Join Call".
   - Both users' video streams will be displayed: local video in the corner, remote video full-screen.

4. **End the Call**:
   - Close the browser tabs to disconnect. The server automatically removes closed connections.

## How It Works
### Technology Stack
- **HTML**: Defines the structure with input fields, buttons, and `<video>` elements for displaying video.
- **CSS**: Styles the video display area, with local video as a small overlay and remote video filling the screen.
- **JavaScript (Client)**:
  - `roomer.js`: Handles the Sender's WebRTC setup, Offer creation, and video stream display.
  - `joiner.js`: Manages the Joiner's connection, Answer generation, and video display.
- **JavaScript (Server)**: `server.js` uses WebSocket to relay signaling data between peers.
- **WebRTC**: Enables peer-to-peer video and audio streaming.
- **WebSocket**: Facilitates real-time signaling for WebRTC negotiation.

### Video Display
- **Local Video**: Displayed in a small, rounded box (`max-width: 20%`, `max-height: 20%`) with a margin and border radius.
- **Remote Video**: Fills the entire screen (`width: 100%`, `height: 100%`) for an immersive experience.
- The `#video-call-div` is hidden by default (`display: none`) and shown dynamically when the call starts.

### Signaling Flow
1. Sender registers a username and creates an Offer.
2. Joiner joins with the same username and receives the Offer.
3. Joiner sends an Answer back to the Sender.
4. ICE Candidates are exchanged to establish the connection.
5. Video streams are displayed once the WebRTC connection is established.

## Configuration
- **WebSocket URL**: Update `ws://192.168.0.118:3000` in `roomer.js` and `joiner.js` to your server's IP address.
- **STUN Servers**: The ICE configuration in `roomer.js` uses public STUN servers. Modify if needed:
  ```javascript
  iceServers: [{ urls: ["stun:stun.aa.net.uk:3478", "stun:stun.cope.es:3478", "stun:stun.demos.ru:3478"] }]
  ```

## Troubleshooting
- **No Video Display**: Ensure camera permissions are granted and the WebSocket server is running.
- **Connection Fails**: Verify the WebSocket URL matches your server's IP and port.
- **CORS Issues**: Serve HTML files via a local server (e.g., `npx http-server`) instead of opening them directly.

## Contributing
Feel free to submit issues or pull requests to improve this project!
