# MARK XXX - AI Assistant Code Structure & Architecture

Repository maintainer: Rohit Ramakant Prajapati
Base: adapted from an open-source JARVIS/Mark-style assistant project

## 📁 Project Architecture Overview

```
MARK-XXX/
├── main.py                          # Entry point - Real-time voice AI loop
├── ui.py                            # User Interface (Jarvis UI)
├── setup.py                         # Installation & Configuration Setup
├── requirements.txt                 # Dependencies
├── config/
│   ├── __init__.py
│   └── api_keys.json               # API Configuration (Gemini API Key)
├── core/
│   └── prompt.txt                  # System Prompt for AI Model
├── memory/
│   ├── __init__.py
│   ├── memory_manager.py           # Persistent Memory Storage (JSON-based)
│   ├── config_manager.py           # Configuration Management
│   └── long_term.json              # Memory Database (Identity, Preferences, Relationships, Notes)
├── agent/
│   ├── planner.py                  # Task Planning & Sequencing (OpenAI-style reasoning)
│   ├── executor.py                 # Task Execution Engine
│   ├── error_handler.py            # Error Detection & Recovery
│   └── task_queue.py               # Task Queue Management
└── actions/                         # Modular Action Handlers (16 modules)
    ├── open_app.py                 # Launch Applications
    ├── browser_control.py          # Browser Automation (Navigation, Clicking, Typing, Scrolling)
    ├── web_search.py               # Web Search & Information Retrieval
    ├── weather_report.py           # Weather Information Fetching
    ├── flight_finder.py            # Flight Search & Booking
    ├── send_message.py             # Message Sending (SMS, Email, etc.)
    ├── reminder.py                 # Create & Manage Reminders
    ├── youtube_video.py            # YouTube Search & Video Control
    ├── computer_control.py         # System Control (Power, Volume, Brightness)
    ├── computer_settings.py        # Windows Settings Management
    ├── file_controller.py          # File & Folder Operations (Create, Copy, Delete, Save)
    ├── desktop.py                  # Desktop Control & Shortcuts
    ├── cmd_control.py              # Command Line Execution (PowerShell/CMD)
    ├── code_helper.py              # Code Analysis & Assistance
    ├── dev_agent.py                # Developer Tools & Scripting
    ├── screen_processor.py         # Screen Analysis & OCR
    └── __pycache__/
```

---

## 🧠 Core Modules Explained

### **1. Main Engine (main.py)**
- **Role**: Central orchestration hub for voice AI
- **Features**:
  - Real-time audio input/output using PyAudio
  - Google Gemini API integration (models/gemini-2.5-flash-native-audio-preview-12-2025)
  - Voice conversation loop
  - Memory integration for contextual awareness
  - Task queue processing
  - Multi-threaded audio handling

### **2. Agent System (agent/)**

#### **Planner (planner.py)**
- Breaks down complex user requests into sequential steps
- Uses AI reasoning to plan optimal task sequences
- Max 5-step planning
- Validates tool availability before planning
- Ensures all steps are independent and executable

#### **Executor (executor.py)**
- Executes planned tasks in sequence
- Handles action dispatch to respective modules
- Generates custom code for complex tasks
- Manages task results and feedback
- Path access: Desktop, Documents, Downloads directories

#### **Error Handler (error_handler.py)**
- Detects execution failures
- Analyzes errors and suggests fixes
- Implements recovery strategies
- Reports error decisions (retry, skip, alternative action)

#### **Task Queue (task_queue.py)**
- Manages pending tasks
- Priority-based execution
- Prevents redundant task execution

### **3. Memory System (memory/)**

#### **Memory Manager (memory_manager.py)**
- **Storage Structure**:
  ```json
  {
    "identity": {},           // User profile data
    "preferences": {},        // User preferences & settings
    "relationships": {},      // Contact information, relationships
    "notes": {}              // General notes & information
  }
  ```
- Thread-safe memory operations
- Persistent JSON storage (`long_term.json`)
- Max 300 chars per value (prevents bloat)
- Recursive update capability

#### **Config Manager (config_manager.py)**
- Manages configuration parameters
- API key handling
- System preferences storage

### **4. Action Handlers (actions/) - 16 Specialized Modules**

| Module | Capability | Functions |
|--------|-----------|-----------|
| **open_app.py** | Application Launcher | Launch any Windows application by name |
| **browser_control.py** | Browser Automation | Navigate URLs, click elements, type text, scroll, extract text, press keys, close tabs |
| **web_search.py** | Web Search Engine | Search the internet for information, compare items, research topics |
| **weather_report.py** | Weather Information | Get current weather, forecasts, temperature, conditions |
| **flight_finder.py** | Flight Booking | Search flights, compare prices, find best deals |
| **send_message.py** | Communication | Send emails, SMS, messaging app messages |
| **reminder.py** | Reminder System | Create reminders, schedule notifications, manage tasks |
| **youtube_video.py** | YouTube Control | Search videos, play/pause, skip, adjust volume |
| **computer_control.py** | System Control | Power on/off, adjust volume, brightness, sleep mode |
| **computer_settings.py** | Windows Settings | Access Windows Settings, adjust configurations |
| **file_controller.py** | File Management | Create files/folders, copy, delete, rename, organize files |
| **desktop.py** | Desktop Control | Access desktop shortcuts, manage desktop items |
| **cmd_control.py** | Command Execution | Run PowerShell/CMD commands, execute scripts |
| **code_helper.py** | Code Assistance | Analyze code, debug, provide programming help |
| **dev_agent.py** | Developer Tools | Development utilities, scripting, automation |
| **screen_processor.py** | Screen Analysis | Capture screenshots, OCR, visual understanding |

### **5. UI System (ui.py)**
- **Jarvis UI**: Visual interface for the AI assistant
- Displays conversation
- Shows task status
- Real-time feedback display

### **6. Configuration (config/)**
- **api_keys.json**: Stores Gemini API credentials
- Secure API key management
- Configuration initialization on first run

### **7. Core Resources (core/)**
- **prompt.txt**: System prompt defining AI behavior, personality, and guidelines

---

## 🎯 All Tasks & Capabilities

### **🗣️ Voice & Communication**
- [x] Real-time voice conversation
- [x] Voice recognition & processing
- [x] Natural language understanding
- [x] Human-like voice response synthesis
- [x] Send messages (SMS, Email)
- [x] Communication automation

### **🌐 Web & Internet**
- [x] Web search & information retrieval
- [x] Browser automation & control
- [x] Website navigation
- [x] Element clicking & interaction
- [x] Text extraction from web pages
- [x] Web form filling
- [x] Weather information fetching
- [x] Flight searching & booking

### **📱 Application Control**
- [x] Launch any Windows application
- [x] YouTube video control (search, play, pause)
- [x] Browser tabs management
- [x] Multi-application orchestration

### **💾 File & System Management**
- [x] Create files and folders
- [x] Copy, delete, rename files
- [x] File organization & sorting
- [x] Desktop management
- [x] Execute system commands (PowerShell/CMD)
- [x] Windows Settings access
- [x] Computer control (power, volume, brightness)

### **📅 Productivity & Organization**
- [x] Create reminders & notifications
- [x] Schedule tasks
- [x] Organize desktop & files
- [x] Multi-step workflow automation

### **👨‍💻 Developer Tools**
- [x] Code analysis & debugging
- [x] Programming assistance
- [x] Custom code generation
- [x] Development automation
- [x] Developer tool integration

### **🖥️ System Intelligence**
- [x] Screen capture & analysis
- [x] Optical Character Recognition (OCR)
- [x] Visual understanding
- [x] Desktop awareness

### **🧠 Memory & Learning**
- [x] Persistent long-term memory
- [x] User preference learning
- [x] Contextual awareness
- [x] Relationship tracking
- [x] Identity persistence
- [x] Memory-based personalization

### **⚙️ Advanced Features**
- [x] Multi-step task planning
- [x] Error detection & recovery
- [x] Autonomous task execution
- [x] Task prioritization
- [x] Adaptive behavior
- [x] Custom code generation for complex tasks
- [x] Context retention across sessions
- [x] Intelligent task sequencing

---

## 🔄 Data Flow Architecture

```
┌─────────────────────┐
│   User Voice Input  │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│ Gemini API (Audio)  │ ◄─────────── Loads memory context
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│  Planner Agent      │ ◄─────────── Breaks down request
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│  Task Queue         │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│   Executor Agent    │ ──────────► Dispatches to Actions
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│ Action Modules (16) │ ──────────► Execute Tasks
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│  Error Handler      │ ◄─────────── Handles failures
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│ Memory Manager      │ ──────────► Stores learning
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│ Voice Response      │ ──────────► User Feedback
└─────────────────────┘
```

---

## 🚀 Technology Stack

- **Language**: Python 3.10+
- **AI API**: Google Gemini (2.5 Flash Native Audio)
- **Audio**: PyAudio
- **Storage**: JSON (Persistent Memory)
- **OS**: Windows 10/11
- **Architecture**: Multi-threaded, Modular, Event-driven

---

## ✅ Summary

**MARK XXX** is a comprehensive personal AI assistant that combines:
- **Voice Interaction** - Natural conversation
- **Task Planning** - Intelligent sequencing
- **Autonomous Execution** - Multi-step workflows
- **System Control** - Deep Windows integration
- **Memory & Learning** - Persistent context awareness
- **Error Recovery** - Intelligent failure handling
- **Extensible Design** - 16+ specialized modules

With **40+ distinct capabilities**, it can handle virtually any user task requiring voice interaction, web access, system control, file management, and intelligent automation.

