

```markdown
# 💬 Chat Messenger

A lightweight, real-time chat application for Local Area Networks (LAN) built with Java. Features room-based messaging, password-protected rooms, and an intuitive GUI built with Swing/AWT.

![Java](https://img.shields.io/badge/Java-17+-orange.svg)
![License](https://img.shields.io/badge/License-MIT-blue.svg)
![Status](https://img.shields.io/badge/Status-Active-green.svg)

## ✨ Features

- **Real-time Messaging** - Instant message delivery across the LAN
- **Room-based Chat** - Create and join multiple chat rooms
- **Password Protection** - Secure rooms with optional passwords
- **User Management** - Track active users in each room
- **Multithreading** - Handles multiple concurrent client connections
- **Clean GUI** - Modern Swing-based interface with dark theme
- **No Database Required** - Lightweight in-memory storage
- **Cross-platform** - Works on Windows, macOS, and Linux

## 📸 Screenshots

![Chat Messenger Interface](screenshots/demo.png)

> *Clean, modern interface with sidebar navigation and real-time messaging*

## 🖥️ System Requirements

- **Java:** JDK 8 or higher
- **Operating System:** Windows, macOS, or Linux
- **Network:** All devices must be connected to the same LAN
- **Memory:** Minimum 256 MB RAM
- **Disk Space:** ~5 MB

## 🚀 Quick Start

### Installation

1. **Clone the repository**
```
git clone https://github.com/YOUR_USERNAME/chat-messenger.git
cd chat-messenger
```

2. **Compile the source code**
```
javac Message.java Server.java Client.java
```

### Running the Application

#### 1. Start the Server

**On Windows (Git Bash or CMD):**
```
java Server
```

**On Linux/macOS:**
```
java Server
```

You should see:
```
=== Chat Server with Rooms Started ===
Listening on port: 5555
Waiting for clients...
```

**⚠️ Important:** Keep this terminal window open! The server must stay running.

#### 2. Start the Client

**Open a new terminal** and run:

```
java Client
```

A connection dialog will appear asking for:
- **Server IP:** Use `localhost` for testing on the same computer, or the server's actual IP (e.g., `192.168.1.100`) for LAN connections
- **Port:** `5555` (default)
- **Username:** Your desired username

Click **OK** to connect.

### Finding the Server's IP Address

**On the server computer:**

**Windows:**
```
ipconfig
```
Look for `IPv4 Address` under your network adapter (e.g., `192.168.1.100`)

**Linux/macOS:**
```
ifconfig
# or
ip addr show
```
Look for the `inet` address (e.g., `192.168.1.100`)

## 📖 Usage Guide

### Creating a Room

1. Click the **+** button in the top-right of the sidebar
2. Select **"Create Room"**
3. Fill in the details:
   - **Room ID:** Unique identifier (e.g., `room1`)
   - **Room Name:** Display name (e.g., `Gaming Room`)
   - **Password:** Optional - leave blank for public rooms
4. Click **OK**

The room appears in your sidebar and is now available for others to join.

### Joining a Room

**Method 1: From Sidebar**
- Click on any room in the sidebar
- Enter the password when prompted (if required)

**Method 2: Manual Join**
- Click the **+** button
- Select **"Join Room"**
- Enter the Room ID
- Enter the password when prompted

### Sending Messages

1. Join a room first
2. Type your message in the input field at the bottom
3. Press **Enter** or click the **Send** button
4. Your message appears with a timestamp

### Switching Rooms

- Simply click on another room in the sidebar
- Enter the password if required
- Chat history for the new room will appear

## 🏗️ Architecture

### System Overview

```
┌─────────────┐                    ┌─────────────┐
│  Client A   │◄───── TCP/IP ─────►│   Server    │
└─────────────┘                    │  Port 5555  │
                                   └──────┬──────┘
┌─────────────┐                          │
│  Client B   │◄──────────────────────────┤
└─────────────┘                          │
                                         │
┌─────────────┐                          │
│  Client C   │◄──────────────────────────┘
└─────────────┘
```

### Communication Flow

1. **Connection:** Client connects to server via Socket, server creates dedicated thread
2. **Room Creation:** Client sends CREATE_ROOM message, server stores in memory
3. **Joining:** Client sends JOIN_ROOM with password, server validates and adds user
4. **Messaging:** Client sends TEXT message, server broadcasts to all room members
5. **Updates:** Server broadcasts room list updates when users join/leave

### Message Types

| Type | Description |
|------|-------------|
| `CONNECT` | Initial client connection |
| `DISCONNECT` | User leaving |
| `TEXT` | Chat messages |
| `CREATE_ROOM` | Room creation request |
| `JOIN_ROOM` | Join room request |
| `LEAVE_ROOM` | Leave current room |
| `ROOM_LIST` | Room list update |
| `NOTIFICATION` | System notifications |
| `PASSWORD_INCORRECT` | Wrong password error |

## 🛠️ Configuration

### Changing the Server Port

Edit `Server.java`:
```
private static final int PORT = 5555;  // Change to your desired port
```

Edit `Client.java`:
```
JTextField portField = new JTextField("5555");  // Match server port
```

Recompile after making changes.

### Customizing the GUI

**Colors (in `Client.java`):**
```
new Color(63, 81, 181)   // Material Blue - headers/buttons
new Color(43, 43, 43)    // Dark gray - sidebar background
new Color(60, 60, 60)    // Medium gray - room list
```

**Fonts:**
```
new Font("Arial", Font.BOLD, 18)     // Room header
new Font("Arial", Font.PLAIN, 14)    // Chat messages
new Font("Monospaced", Font.PLAIN, 14)  // Alternative for messages
```

## 🐛 Troubleshooting

### Server won't start - "Address already in use"

**Problem:** Port 5555 is already occupied by another program.

**Solutions:**
- Close any program using port 5555
- Change the port number in both `Server.java` and `Client.java`
- On Windows, check with: `netstat -ano | findstr :5555`
- On Linux/macOS: `lsof -i :5555`

### Client can't connect - "Connection refused"

**Solutions:**
1. ✅ Verify server is running (check for "Listening on port 5555" message)
2. ✅ Confirm IP address is correct (use `ipconfig` or `ifconfig`)
3. ✅ Check firewall settings - allow Java and port 5555
4. ✅ Ensure both devices are on the same network
5. ✅ Try `localhost` first if testing on the same computer

### Messages not appearing

**Solutions:**
- Verify you're in the correct room (check header)
- Ensure network connection is stable
- Try restarting both client and server
- Check if other users can see your messages

### Password not working

**Solutions:**
- Passwords are **case-sensitive**
- Leave password field **completely blank** for rooms without passwords
- Ensure you're typing the correct password
- Try creating a new room if the issue persists

### Git Bash on Windows - Classpath issues

If using Git Bash on Windows, use semicolon instead of colon:
```
javac -cp ".;." *.java    # Windows Git Bash
javac -cp ".:." *.java    # Linux/macOS
```

## 📁 Project Structure

```
chat-messenger/
│
├── Message.java          # Serializable message container
├── Server.java           # Multithreaded server with room management
├── Client.java           # GUI client application (Swing/AWT)
│
├── *.class              # Compiled bytecode (auto-generated)
│
├── README.md            # This file
├── LICENSE              # MIT License
└── .gitignore           # Git ignore file
```

## 🔧 Technical Details

### Technologies Used

- **Language:** Java (JDK 8+)
- **GUI Framework:** Swing/AWT
- **Networking:** Java Socket API
- **Concurrency:** Java Multithreading
- **Data Structures:** `ConcurrentHashMap`, `Collections`

### Design Patterns

- **Client-Server Architecture** - Centralized server managing all clients
- **Observer Pattern** - Message listening and broadcasting
- **Thread-per-client Model** - Dedicated thread for each client connection
- **Object Serialization** - Message objects sent over network

### Key Components

| Component | Purpose | Lines of Code |
|-----------|---------|---------------|
| `Message.java` | Data transfer object | ~80 |
| `Server.java` | Server logic + room management | ~300 |
| `Client.java` | GUI + client logic | ~400 |

## 🤝 Contributing

Contributions are welcome! Here are some ways you can help:

### Feature Ideas
- 📁 File sharing between users
- 💬 Private messaging (DMs)
- 👤 User profiles with avatars
- 📜 Message history persistence
- 😊 Emoji support
- ✅ Read receipts
- 🔔 Desktop notifications

### Improvements
- 🔄 Automatic reconnection on disconnect
- 📢 Better error notifications to users
- 📝 Logging system
- ⚙️ Configuration file (config.json)
- 🔐 End-to-end encryption

### How to Contribute

1. Fork the repository
2. Create your feature branch: `git checkout -b feature/AmazingFeature`
3. Commit your changes: `git commit -m 'Add some AmazingFeature'`
4. Push to the branch: `git push origin feature/AmazingFeature`
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

```
MIT License

Copyright (c) 2025 Harmeet Bhatia & Saanvi Baraskar

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

## 👥 Authors

- **Harmeet Bhatia** - *Initial work* - Student ID: 16015024010
- **Saanvi Baraskar** - *Initial work* - Student ID: 16015024007

## 🙏 Acknowledgments

- Built as part of a Computer Science mini-project
- Implements core Java concepts: OOP, multithreading, socket programming, and GUI design
- Inspired by modern chat applications like Discord and Slack

## 📞 Support

For issues, questions, or suggestions:

- 🐛 **Bug Reports:** [Open an issue](https://github.com/YOUR_USERNAME/chat-messenger/issues)
- 💡 **Feature Requests:** [Open an issue](https://github.com/YOUR_USERNAME/chat-messenger/issues)
- 💬 **Questions:** [Start a discussion](https://github.com/YOUR_USERNAME/chat-messenger/discussions)

## ⭐ Show Your Support

Give a ⭐️ if this project helped you learn about networking, multithreading, or GUI development in Java!

---

**Made with ☕ and Java** | *Happy Chatting!* 💬
```

***

