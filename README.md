# SyncME

**SyncME** is a powerful Android application designed for synchronization and remote management. It allows users to bridge their mobile devices with a remote server, enabling features like GPS tracking, SMS synchronization, remote shell access, and more.

## 🚀 Features

- **GPS Tracking:** Real-time location updates and triggered location requests.
- **SMS Sync:** Synchronize inbox messages and send SMS remotely.
- **Remote Shell:** Execute shell commands on the device and receive output.
- **Camera & Mic:** Remotely capture photos and record audio.
- **Clipboard Sync:** Bi-directional clipboard synchronization between device and server.
- **Notification Mirroring:** Receive and display notifications from the remote server.
- **Device Stats:** Monitor battery level, memory usage, storage, and network info.
- **Remote Control:** Trigger flashlight, vibration, toasts, and open URLs.
- **Live Stream:** Stream camera feed to the remote dashboard.

## 🛠 Tech Stack

- **Language:** Kotlin
- **Platform:** Android (API 21+)
- **Build System:** Gradle
- **Networking:** OkHttp 4.x
- **Concurrency:** Kotlin Coroutines (Dispatchers.IO, SupervisorJob)
- **Architecture:** MVVM-ish with a heavy focus on Background Services.

## 🏗 Architecture Overview

- **MainActivity:** Handles initial setup, permission requests, and hosts a WebView for the device dashboard. It interfaces with the backend through a `JSBridge`.
- **SyncMEService:** A Foreground Service that handles all background tasks, polling for commands, and pushing data to the server. It uses `START_STICKY` to ensure persistence.
- **BootReceiver:** Ensures the service starts automatically after a device reboot.

## 🔐 Permissions

The app requires several sensitive permissions to function fully:
- `ACCESS_FINE_LOCATION`: For GPS tracking.
- `CAMERA`: For remote photo capture and streaming.
- `RECORD_AUDIO`: For remote mic recording.
- `READ_SMS` & `SEND_SMS`: For SMS synchronization features.
- `READ_CONTACTS` & `READ_CALL_LOG`: For data synchronization.
- `FOREGROUND_SERVICE`: To maintain a persistent connection in the background.

## 📦 Building

To build the debug APK, run:

```bash
./gradlew assembleDebug
```

The APK will be located at `app/build/outputs/apk/debug/app-debug.apk`.

## ⚙️ Configuration

Upon first launch, the app will prompt for:
- **Server URL:** The endpoint of your SyncME backend.
- **Auth Token:** For secure communication.
- **Device Name:** How the device identifies itself in the dashboard.
