# LLM-Enabled Drone GCS  
_A Ground Control Station Project with Integrated STT, LLM, and Vision Metadata for Defense Applications_

## Project Overview

This repository documents the development of an advanced Ground Control Station (GCS) for drones, integrating Speech-to-Text (STT), Large Language Model (LLM), and vision-based metadata processing. The system is designed for defense applications, providing secure, robust, and intelligent drone operations via natural language commands and automated mission report generation.

## System Architecture

### Workflow Diagram

```
[Speech Input]
      ↓
[STT Engine]
      ↓
[LLM (Intent Parsing)]
      ↓
[Mission/Event Generation]
      ↓
[GCS/SDK Execution]
      ↓
[Vision Encoder]
      ↓
[Metadata Transmission]
      ↓
[LLM Report Generation]
```

### Key Components

- **Speech-to-Text (STT):**  
  Evaluates and integrates Google Speech Recognition, Vosk, and OpenAI Whisper for robust Korean command transcription.

- **Large Language Model (LLM):**  
  Fine-tuned to interpret transcribed commands and generate mission events.

- **Event System:**  
  Converts LLM outputs into structured tasks for the drone GCS or SDK.

- **Vision Encoder:**  
  Onboard processing of exploration metadata (e.g., detected objects, terrain).

- **Automated Reporting:**  
  LLM synthesizes mission logs and metadata into structured reports.

## Features

- **Multi-Engine STT Integration:**  
  Accurate transcription of Korean drone commands, even in noisy or complex scenarios.

- **LLM-Based Command Understanding:**  
  Flexible, context-aware mission generation from natural language.

- **Event and Mission Creation:**  
  Structured, automatable tasks for execution by the drone system.

- **Vision Metadata Fusion:**  
  Real-time encoding and transmission of environmental data.

- **Automated Exploration Reports:**  
  End-to-end mission documentation for post-operation analysis.

- **Defense-Grade Security:**  
  Offline capability, local model execution, and minimal network dependency.

## Example Images

### 1. System Architecture Overview

![System Architecture Diagram](https://user-images.githubusercontent.com/yourrepo/architecture 2. STT Workflow

![STT Workflow Example](https://user-images.githubusercontent.com/yourrepo/stt-workflow Encoder Output

![Sample Vision Metadata](https://user-images.githubusercontent.com/yourrepo/vision-metadata Results

| Task                        | Google Speech Recognition | Vosk           | OpenAI Whisper   |
|-----------------------------|--------------------------|----------------|------------------|
| "이륙해"                    | [Insert result]          | [Insert result]| [Insert result]  |
| "이륙하고 고도 10미터 유지" | [Insert result]          | [Insert result]| [Insert result]  |
| "앞으로 100미터 전진"        | [Insert result]          | [Insert result]| [Insert result]  |

## Getting Started

1. **Clone the Repository**
   ```bash
   git clone https://github.com/yourorg/llm-drone-gcs.git
   ```

2. **Install Dependencies**
   - Python 3.8+
   - [Google Speech Recognition](https://pypi.org/project/SpeechRecognition/)
   - [Vosk](https://alphacephei.com/vosk/)
   - [OpenAI Whisper](https://github.com/openai/whisper)
   - [sounddevice](https://python-sounddevice.readthedocs.io/)
   - [ffmpeg](https://ffmpeg.org/)

3. **Configure Models**
   - Download and set up Korean models for Vosk and Whisper.
   - Ensure ffmpeg is installed and accessible in your PATH.

4. **Run Example Code**
   - See `/stt/`, `/llm/`, and `/vision/` directories for scripts and usage.

## Defense-Oriented Design

- **Mission-Critical Reliability:**  
  All modules are tested for robustness in operational scenarios.

- **Offline and Secure Operation:**  
  Local model execution ensures privacy and compliance.

- **Scalable and Modular:**  
  Easily adaptable for various drone platforms and mission types.

## Contribution

- Fork the repo and submit pull requests for new features, bug fixes, or documentation.
- Open issues for feedback or feature requests.

## License

This project is licensed under the MIT License.

## References

- [Google Speech Recognition Documentation]
- [Vosk Speech Recognition]
- [OpenAI Whisper]
- [FFmpeg]

: https://pypi.org/project/SpeechRecognition/  
: https://alphacephei.com/vosk/  
: https://github.com/openai/whisper  
: https://ffmpeg.org/  

## Contact

For collaboration or questions, please contact the maintainer at `your.email@domain.com`.
