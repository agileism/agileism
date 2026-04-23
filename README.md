# Hi, I'm Jakob Cruz
Senior Software Engineer based in **Victoria, BC**. I build and scale modern cloud applications and enjoy simplifying complexity with clean architecture, smart automation, and strong developer experience.

- **Address**: `Vancouver, BC, Canada`
- **LinkedIn**: [jakob-paul-cruz](https://www.linkedin.com/in/jakob-paul-cruz)

## What I do
- **Full-stack delivery**: architecture → database design → APIs → deployment
- **Performance & reliability**: pragmatic engineering, measurable outcomes, steady ops
- **Cloud & CI/CD**: containerized infrastructure and automation that reduces busywork

## Tech I use (a lot)
- **Languages**: Python, Go, TypeScript/JavaScript
- **Backend**: Django, Flask, FastAPI, Wagtail, gRPC
- **Frontend**: Vue/Nuxt, React/Next
- **Data**: Postgres, MySQL, MongoDB, DynamoDB
- **Infra**: Docker, Kubernetes, Terraform, Jenkins
- **Cloud**: GCP, AWS, Azure (plus Linode/Divio)

## Experience highlights
### BC Public Service — Senior Software Engineer (Apr 2020 – Present)
- Modernized legacy applications with **Python 3 + Nuxt**, including refactoring a monolithic Flask app into **microservices** and migrating from **OpenShift → GCP**.
- Built an **AI-driven document/form service** to sanitize and convert uploads to PDF, cutting ongoing costs from “thousands” to **under $1k**.
- Led a multi-repo integration effort (7 repos), coordinating across teams and shipping on a consistent demo cadence.

### Synic Software — Software Engineer (Jul 2015 – Apr 2020)
- Backend lead work: roadmap/PI planning, stakeholder communication, and mentoring.
- Built and scaled a **microservice API** (up to **35k QPS**) using **Python/Go** with stress & integration testing.
- Delivered an AI-driven contactless healthcare screening platform (React/Go/Python) deployed on **GCP**.
- Revamped CMS platforms (WordPress → Wagtail; headless architectures with Next/Vue).

## A small, honest “funny” section
- I like **removing busywork** so much that I’ll happily automate myself out of a recurring meeting.
- I’m fluent in **“it works on my machine”** *and* “here’s the reproducible steps + metrics.”
- If you bring a gnarly legacy system, I bring **patience**, **tests**, and **a plan**.

## Currently interested in
- Platforms that make developers faster: **DX, tooling, CI/CD, internal platforms**
- **Cloud-native** architectures, pragmatic AI integrations, and strong engineering culture

---
If you’re building something that should feel effortless to operate, I’d love to help.
# Interview Companion - Windows Audio Transcription Application

## Overview

Interview Companion is a Windows desktop application that captures system audio output and provides real-time transcription using AI. It features voice activity detection (VAD) for automatic recording and transcription during interviews.

## Features

- **System Audio Capture**: Captures audio from the default Windows audio output device using WASAPI loopback
- **Session Transcription**: Records the full session and transcribes once you stop
- **Device Management**: Lists and allows selection of system audio output devices
- **Secure API Key Storage**: Stores API keys locally in Windows Registry with basic encryption
- **Activity Log**: Displays step-by-step status updates inside the app

## Requirements

- Windows 10/11
- .NET 10.0 Runtime
- Google Gemini API key
- An active audio output device

## Building the Application

1. Ensure you have .NET 10.0 SDK installed
2. Open a terminal in the project directory
3. Run: `dotnet restore`
4. Run: `dotnet build`
5. Run: `dotnet run` or build the executable

## Usage

1. **Launch the Application**: Start InterviewCompanion.exe
2. **Enter API Key**: Enter your Google Gemini API key in the secure field (or use the default provided)
3. **Select Audio Device** (Optional): Choose your preferred audio output device from the list
4. **Start Transcription**: Click "Start Transcription" to begin capturing and transcribing audio
5. **Stop Transcription**: Click "Stop Transcription" to finish recording and start transcription
6. **View Transcript**: The transcript appears once processing finishes; clear it with "Clear" when needed
7. **Activity Log**: Monitor step-by-step status messages in the Activity Log panel

## Technical Details

### Architecture

- **Framework**: WPF (.NET 10.0)
- **Audio Library**: NAudio (WASAPI loopback capture)
- **API Integration**: Google Gemini REST API
- **Settings Storage**: Windows Registry (HKEY_CURRENT_USER\Software\InterviewCompanion)

### Audio Processing

- Uses WASAPI loopback capture to record system audio output
- Captures audio in the system's native format during the entire session
- Converts the complete session to WAV format (LINEAR16 PCM) for API transmission on stop

### API Integration

- Endpoint: `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.0-flash-exp:generateContent`
- Format: WAV audio (base64 encoded)
- Model: Gemini 2.0 Flash (Experimental)
- Features: Multimodal AI transcription with automatic punctuation

## Important Notes

### Virtual Audio Device Limitation

Creating a true virtual audio device on Windows (like Black Hole on macOS) requires kernel-mode driver development, which is complex. This application uses **WASAPI loopback capture** instead, which:

- Captures audio from the default playback device
- Works without requiring additional drivers
- Provides similar functionality for transcription purposes

If you need a true virtual device, consider using third-party solutions like:
- VB-Audio Virtual Cable
- Virtual Audio Cable

### Setting Default Audio Device

The application attempts to set the default audio device programmatically, but this may require administrator privileges. If it fails, you can manually set the default device in Windows Sound Settings, and the application will detect the change.

## File Structure

```
InterviewCompanion/
├── InterviewCompanion.csproj    # Project file
├── App.xaml / App.xaml.cs      # Application entry point
├── MainWindow.xaml / .cs       # Main UI window
├── Models/
│   └── AudioDevice.cs          # Audio device model
├── Services/
│   ├── AudioDeviceService.cs   # Device enumeration and management
│   ├── AudioCaptureService.cs  # WASAPI loopback capture
│   ├── TranscriptionService.cs # Google API integration
│   └── SettingsService.cs      # API key storage
└── README.md                    # This file
```

## Troubleshooting

### No Audio Devices Found
- Ensure audio drivers are installed
- Check Windows Sound Settings
- Try clicking "Refresh Devices"

### Transcription Not Working
- Verify your API key is correct
- Check internet connection
- Ensure audio is playing on the selected device
- Check the status message for error details

### Permission Errors
- Some operations may require administrator privileges
- Try running the application as administrator if device selection fails

## License

This project is provided as-is for development purposes.

## API Key

The application includes a default API key for testing. For production use, replace it with your own Google Gemini API key.

