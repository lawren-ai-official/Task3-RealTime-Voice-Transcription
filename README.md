# Task3-RealTime-Voice-Transcription

## Repository Setup and Access

Before you begin work on this task, please follow these steps:

1. **Create a New Repository**
   In your GitHub account, create a new **private** repository for this project.

2. **Grant Access**
   Add the users specified in the invitation email as collaborators (with at least read access) to your repository *before the deadline*.

---

## Overview

Build a fully local, real-time speech-to-text application in **Rust** that captures audio from the user’s microphone and transcribes it on-the-fly. You can use one of the recommended libraries or one of your choosing. We recommend:

* **Whisper** (via a Rust binding such as `whisper-rs` or `whisper.cpp`), or
* A Kaldi-based engine (e.g., via the `vosk` Rust crate).

Your application will:

1. **Capture Audio**
   Continuously read from the system microphone with minimal latency using a crate like `cpal`.

2. **Voice Activity Detection (VAD)**
   Segment the incoming stream into speech versus silence via a Rust VAD binding (e.g., `webrtc-vad-rs`).

3. **Transcribe**
   Send each detected speech segment to your local ASR engine (Whisper or Vosk/Kaldi), handling partial and final hypotheses.

4. **Stream Output**
   Display partial and finalized transcripts in real time in a terminal UI (TUI) using `ratatui` or `tui-rs`.

5. **Persist**
   Append completed transcripts to a rolling log file, and support on-demand export to `.txt`, `.json`, and `.srt`.

6. **Control Interface**
   Provide a CLI/TUI interface with commands to start/stop/pause/resume transcription and adjust parameters (e.g., VAD aggressiveness, model size).

7. **Configuration & Extensibility**
   Load defaults from a `config.yaml` (via `serde_yaml`), and structure the code so users can swap in alternative VAD or transcription engines easily.

> **Note on Test Data:**
> Include at least three short WAV or FLAC recordings (1–2 minutes each) in a `/samples` folder. Write unit tests (with `cargo test`) to validate VAD segmentation and transcription correctness on these fixtures.

---

## Recommended Preparation Materials

* [Rust Ramp-Up Guide](https://github.com/lawren-ai-official/programming_challenge_preparation_materials/blob/main/preparation_materials/rust_ramp_up.md) – Core Rust concepts
* [Cursor AI Guide](https://github.com/lawren-ai-official/programming_challenge_preparation_materials/blob/main/preparation_materials/technology_guides/cursor_ai_guide.md) – Leveraging AI for development
* [Database Integration Guide](https://github.com/lawren-ai-official/programming_challenge_preparation_materials/blob/main/preparation_materials/technology_guides/database_integration_guide.md) – PostgreSQL, Redis, QDrant integration

If you're building a web interface:

* [Leptos Introduction](https://github.com/lawren-ai-official/programming_challenge_preparation_materials/blob/main/preparation_materials/leptos_introduction.md) – Full-stack web development

If you’re coming from another language:

* [Language Transition Guides](https://github.com/lawren-ai-official/programming_challenge_preparation_materials/tree/main/preparation_materials/language_transition_guides)

---

## `.specstory` Files Requirement

**IMPORTANT:** Use Cursor AI throughout development. Maintain `.specstory` files under `/specs` to document all prompt engineering, code generation, and debugging sessions. Commit them alongside your code.

---

## Points System

| Feature                                        | Points |
| ---------------------------------------------- | ------ |
| **Real-Time Audio Capture (cpal)**             | 50     |
| **Voice Activity Detection Integration**       | 50     |
| **Local Whisper/Kaldi Transcription**          | 100    |
| **Streaming Partial & Final Outputs**          | 50     |
| **CLI/TUI Control Interface (ratatui/tui-rs)** | 25     |
| **Config File & Modular Architecture**         | 25     |
| **Transcript Export (TXT/JSON/SRT)**           | 25     |
| **Logging & Robust Error Handling**            | 25     |
| **Sample Audio Fixtures & Unit Tests**         | 25     |
| **Optional GUI (eg. egui, iced)**              | 50     |
| **Dockerization for Local Deployment**         | 25     |
| **Test Coverage & CI Integration**             | 50     |
| **Comprehensive Documentation**                | 50     |

> **Minimum required score:** 200 points

---

## Core Requirements

1. **Audio Capture**

   * Use `cpal` to capture 16 kHz (or higher) mono audio from the default microphone with low buffer latency.
   * Ensure cross-platform support (Linux, macOS, Windows).

2. **Voice Activity Detection**

   * Integrate `webrtc-vad-rs` to detect speech boundaries in the audio stream.
   * Emit segments after configurable pre/post-speech padding.

3. **Transcription Integration**

   * Invoke Whisper locally via `whisper-rs` or `whisper.cpp` FFI, or use Vosk via `vosk-rs`.
   * Handle streaming or chunked audio input to surface partial transcription results in real time.
   * Allow switching model variants (tiny, base, small, etc.) via `config.yaml`.

4. **Streaming Results**

   * Render interim and final transcripts in a scrolling TUI view, updating in place.
   * Use `ratatui` (or `tui-rs`) to build a responsive terminal interface.

5. **CLI/TUI & Controls**

   * Commands:

     * `start`: begin capturing and transcribing
     * `stop`: end the session
     * `pause`/`resume`: temporarily suspend/resume audio input
     * `set-config <key> <value>`: adjust runtime parameters
     * `export-transcript [--format txt|json|srt]`
   * Display status: elapsed time, model in use, VAD mode, error notifications.

6. **Export & Persistence**

   * Append each finalized segment to a rolling transcript file.
   * On `--export`, dump full session transcripts to `.txt` (plain), `.json` (with timestamps), and optional `.srt` subtitle files.

---

## Optional Enhancements

* **Speaker Diarization** via a Rust diarization crate or integrating external tools.
* **Live Translation** by piping transcripts through a local translation model.
* **Noise Suppression** front-end using `rnnoise` Rust bindings.
* **Wake-Word Detection** to trigger transcription after a hotword.
* **WebSocket Streaming** to a local web dashboard.
* **Multi-Language Support** with auto-language detection and dynamic model loading.

---

## Evaluation Criteria

1. **Functionality**: Real-time capture, VAD, transcription, streaming UI.
2. **Code Quality**: Modular Rust architecture, error handling, readability.
3. **Local Model Integration**: Ease of swapping Whisper/Kaldi, performance trade-offs.
4. **User Experience**: Intuitive TUI/CLI, smooth updates, clear controls.
5. **Points Achieved**: Submission meets or exceeds 200 points.

---

## Submission Requirements

Please provide:

1. **Source Code** in your private GitHub repository
2. **Setup Instructions** (dependencies, model downloads, build steps)
3. **Technical Document** detailing:

   * Architectural overview
   * Crate choices and trade-offs
   * How AI/ASR models were integrated
   * Points breakdown of implemented features
4. **.specstory Files** under `/specs`, documenting:

   * Prompt engineering and code generation interactions
   * Debugging sessions guided by AI
   * Iterative design decisions and AI-assisted solutions

Good luck! Remember, we're more interested in your problem-solving approach and how you leverage AI tools than in a perfect implementation. Choose an approach that allows you to demonstrate your strengths while completing the task within the 3-day timeframe.
