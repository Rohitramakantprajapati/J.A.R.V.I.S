# JARVIS Project Master Note (Capabilities, Libraries, Architecture, Interview Prep)

## Attribution

This repository is an adapted/customized version of an existing open-source JARVIS/Mark-style assistant.
Current repository maintenance and custom updates are by Rohit Ramakant Prajapati.

## 1) Project Snapshot

Project name: Jarvis (MARK XXX lineage)

Goal: Build a real-time Windows AI assistant that can listen, reason, speak, and execute tasks on the computer using modular tools.

Core value:
- Real-time voice conversation with low-latency responses
- Tool-use based automation (apps, browser, files, reminders, messaging, search)
- Visual interaction modules (screen/camera processing)
- Persistent memory for personalized behavior
- Agent-style planning/execution for multi-step tasks

Target platform:
- Windows 10/11
- Python 3.10+


## 2) What This Project Can Do

### Voice + Conversation
- Capture microphone audio in real time
- Stream input to Gemini live model
- Receive streaming audio output from model and play it back
- Show transcribed user/assistant turns in UI log

### System and Desktop Automation
- Open applications by name
- Run command-line tasks through controlled command action
- Desktop/UI automation through keyboard, mouse, typing, scrolling, screenshots
- Focus windows, clear fields, and smart typing patterns for forms

### Browser and Web Intelligence
- Browser automation using Playwright (navigation, interactions)
- Web search action (Gemini search tool, DDG fallback)
- Fetch useful online information and compare items

### Daily Utility Tasks
- Weather reports
- Reminders and local notification behavior
- Sending messages via app UI automation
- YouTube play/summarize/info style actions
- Flight discovery helper action

### Developer and Agent Workflows
- Planner and executor modules for multi-step goals
- Error analysis + potential fix suggestions
- Code-helper and dev-agent style modules

### Memory and Personalization
- Long-term memory file structure (identity, preferences, relationships, notes)
- Periodic memory extraction from conversation
- Prompt enrichment with memory context and current date/time


## 3) End-to-End Pipeline (How It Works)

1. App boot:
- main.py starts UI and background runner thread
- API key check and prompt loading

2. Live connection:
- Creates Gemini live session with system instruction + tools
- Starts four async loops:
  - send realtime input
  - listen mic
  - receive server events/audio/transcripts/tool calls
  - play output audio

3. User interaction:
- Microphone chunks are streamed continuously
- Model transcribes and responds
- Output audio chunks are played to speakers

4. Tool calling:
- If model triggers function calls, dispatcher routes to matching action module
- Action returns result payload
- Result is sent back to model as function response

5. Memory update:
- Every N turns, user text is checked for personal facts
- Structured memory is extracted and merged

6. Resilience:
- Connection errors are caught
- Loop reconnects automatically after delay


## 4) Folder-by-Folder Understanding

### Root Files
- main.py: real-time orchestrator, tool dispatcher, live audio session lifecycle
- ui.py: animated Jarvis interface, logs, setup overlay, status visualization
- setup.py: installs Python deps and Playwright browser binaries
- requirements.txt: external dependencies
- readme.md: user-facing project intro and setup steps
- AI_STRUCTURE_DOCUMENTATION.md: architecture explanation

### actions/
Contains modular task handlers. Main examples:
- open_app.py: app launch logic
- browser_control.py: Playwright browser operations
- web_search.py: Gemini search + DDG fallback
- weather_report.py: weather retrieval logic
- send_message.py: app-level messaging automation
- reminder.py: reminder/toast style behavior
- youtube_video.py: YouTube related operations
- computer_control.py: generic OS UI actions (click/type/hotkey/screenshot/etc)
- computer_settings.py: settings-level controls
- file_controller.py: file create/move/delete with recycle-bin behavior
- cmd_control.py: guarded command execution
- screen_processor.py: screen/camera processing + model interactions
- code_helper.py: coding assistance workflows
- dev_agent.py: development automation helper
- flight_finder.py: flight search helper
- desktop.py: desktop-focused automation flow

### agent/
- planner.py: creates tool/action plan for goals
- executor.py: executes plan steps and handles outcomes
- error_handler.py: analyzes failures and recovery paths
- task_queue.py: priority queue and worker management

### memory/
- memory_manager.py: load, merge, format long-term memory
- config_manager.py: configuration support

### config/
- api_keys.json: runtime API key storage

### core/
- prompt.txt: base system behavior instructions


## 5) Library-to-Purpose Map (Important for Interview)

External dependency map from requirements and code usage:

- pyaudio:
  - Real-time microphone capture and speaker playback
  - Used by main live loop and screen processor voice path

- google-genai:
  - Live and modern Gemini client interfaces
  - Used for live audio model sessions and content generation in some actions

- google-generativeai:
  - Additional Gemini usage in planner/executor/error handling/memory extraction
  - Used for structured prompting and fallback generation patterns

- pillow:
  - UI face image processing and general image manipulations
  - Used in ui.py and image pre-processing paths

- requests:
  - HTTP requests for utility modules where API calls or page fetches are needed

- beautifulsoup4:
  - HTML parsing for web-derived content extraction

- playwright:
  - Browser automation (navigation, search pages, clicks, interactions)

- pyautogui:
  - Desktop automation (mouse, keyboard, screenshots)
  - Core for open_app/send_message/computer_control/youtube interactions

- pyperclip:
  - Clipboard copy/paste acceleration for automation flows

- opencv-python (cv2):
  - Camera/screen frame handling and image conversion

- numpy:
  - Array/image support in video/screen processing modules

- mss:
  - Fast screen capture

- psutil:
  - Process inspection and app-state checks

- send2trash:
  - Safe delete to recycle bin instead of permanent unlink

- comtypes:
  - Windows COM interop support (often used in system audio/control flows)

- pycaw:
  - Windows Core Audio controls (volume/session device control)

- win10toast:
  - Native Windows toast notifications for reminder flow

- duckduckgo-search:
  - Search fallback provider when Gemini search fails

- youtube-transcript-api:
  - YouTube transcript extraction for summarize/info features


## 6) Technical Design Decisions You Can Explain

- Modular action architecture:
  - New capability can be added as a new action file and function declaration
  - Reduces coupling and keeps orchestration clean

- Tool-first execution:
  - Assistant is instructed to call tools rather than hallucinate task completion

- Async + threads hybrid:
  - Async tasks handle live IO streams
  - Threads used for UI + background helpers + non-async action wrappers

- Memory write throttling:
  - Memory extraction is periodic (every N turns) to reduce cost and noise

- Defensive imports:
  - Safe import wrappers allow startup even if optional dependencies fail

- Automatic reconnect:
  - Live session reconnect loop improves robustness for network/API hiccups


## 7) What To Say In an Interview (Short Script)

Use this 60-90 second answer:

"I built a Windows-focused real-time AI assistant in Python. The system streams microphone audio to a Gemini live model and plays streaming voice responses back to the user. It supports tool calling through a modular action layer for app launch, browser automation, file operations, reminders, messaging, and visual processing. I designed it with async streaming loops for low-latency audio, plus a task-agent layer (planner, executor, error handler) for multi-step autonomy. I also added persistent long-term memory with structured categories so the assistant can personalize responses over time. The architecture is fault-tolerant with guarded imports and reconnect behavior, and it is easy to extend by adding new action modules and tool declarations." 


## 8) Interview Questions and Model Answers

### Q1. What problem does this project solve?
A: It converts a normal Windows PC into a voice-driven automation assistant that can understand commands and execute real actions across apps, browser, and system workflows.

### Q2. Why did you choose a modular action architecture?
A: It isolates responsibilities, improves maintainability, and allows independent extension/testing of capabilities without rewriting core orchestrator logic.

### Q3. How does the audio pipeline work?
A: Mic audio chunks are captured with PyAudio, streamed to the live model, response audio chunks are received asynchronously, then written to an output stream for playback.

### Q4. Why use async plus threads together?
A: Async handles concurrent IO streams efficiently, while threads are useful for UI loop separation and wrapping blocking code paths.

### Q5. How are tool calls executed safely?
A: A dispatcher maps model tool names to known action functions. Unknown tools are rejected, and action failures are wrapped with error responses.

### Q6. How do you reduce hallucination?
A: The system prompt biases tool use, and task execution returns real function outputs back to the model instead of relying on invented responses.

### Q7. How is user memory managed?
A: Memory is JSON-based with fixed categories. A periodic extraction step pulls personal facts and merges updates with thread-safe handling.

### Q8. What are the biggest failure points in this architecture?
A: API outages, microphone/speaker device conflicts, automation selector fragility, and third-party app UI changes.

### Q9. How do you recover from runtime failures?
A: Catch and log exceptions, reconnect live session automatically, and use fallback providers (e.g., DDG for search).

### Q10. Why include both google-genai and google-generativeai?
A: Different modules currently rely on different SDK patterns. A future refactor can unify clients for consistency.

### Q11. How would you test this project?
A: Unit tests for utility/action logic, integration tests for dispatcher/tool response contracts, and manual e2e checks for audio and automation workflows.

### Q12. How do you prevent dangerous command execution?
A: The cmd action uses blocked pattern checks and controlled generation/execution flow rather than blindly executing arbitrary input.

### Q13. How scalable is this design?
A: For single-user desktop usage it is strong. Horizontal scaling would require decoupling UI/device dependencies and moving runtime components into services.

### Q14. How do you handle latency?
A: Streaming audio and incremental receive loops reduce perceived delay versus request/response batch processing.

### Q15. What security concerns exist?
A: API key storage, command execution risks, and automation permissions. Better secret management and stricter policy checks are recommended.

### Q16. What did you optimize most in this build?
A: Responsiveness and practicality: low-latency interaction, direct tool execution, and robust fallback behavior.

### Q17. How does the planner/executor layer help?
A: It decomposes large user goals into manageable steps, improving completion reliability for multi-stage tasks.

### Q18. Why is persistent memory useful here?
A: It enables personalized assistant behavior across sessions, reducing repetitive user setup and improving user experience.

### Q19. If given more time, what would you improve first?
A: Add automated tests, stronger policy sandboxing, structured observability, and consolidate Gemini SDK usage.

### Q20. What is your proudest engineering aspect in this project?
A: Integrating real-time voice streaming, tool automation, memory, and agent planning into one practical assistant architecture.


## 9) Strengths, Limitations, and Improvement Roadmap

Strengths:
- Practical, real-world automation coverage
- Good architectural separation
- Real-time conversational UX
- Extensible tool system

Current limitations:
- Heavy dependence on Windows desktop state for GUI automation
- External API and internet dependency for core intelligence
- Limited automated regression test coverage

Roadmap:
- Add action-level test harness and mockable adapters
- Add structured logging and metrics dashboards
- Introduce permission model and policy layer for sensitive tools
- Unify Gemini SDK clients
- Improve onboarding diagnostics for mic/speaker/API setup


## 10) Quick Resume Bullet Points (Use Directly)

- Built a real-time Python voice assistant on Windows with streaming AI audio input/output.
- Designed modular tool-calling architecture with 16+ action handlers for browser, file, messaging, and system automation.
- Implemented agent-style planning, execution, and error-handling pipeline for multi-step task completion.
- Added persistent long-term memory and context injection for personalized interactions across sessions.
- Integrated fallback mechanisms and reconnect logic to improve reliability in live operation.


## 11) One-Line Summary

This project is a modular, real-time, voice-first desktop AI assistant that combines live conversation, tool-based automation, memory, and multi-step agent execution into a single Windows productivity system.
