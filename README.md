# LLM-Enabled Drone GCS  
_A Ground Control Station Project with Integrated STT, LLM, and Vision Metadata for Defense Applications_

## Project Overview

This repository documents the development of an advanced Ground Control Station (GCS) for drones, integrating Speech-to-Text (STT), Large Language Model (LLM), and vision-based metadata processing. The system is designed for defense applications, providing secure, robust, and intelligent drone operations via natural language commands and automated mission report generation.

## System Architecture

### Workflow Overview

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
[Vision Encoder (YOLOv8)]
      ↓
[Metadata Transmission]
      ↓
[LLM Report Generation]
```

## Hardware Platform

### Drone Platform: DJI Matrice 400 (M400)

- **Type:** Industrial-grade quadcopter
- **Payload Capacity:** High, suitable for various sensors and onboard computers
- **Flight Time:** Extended endurance for professional missions
- **Key Features:**
  - Advanced obstacle avoidance
  - Multi-payload support
  - High-precision RTK positioning
  - Integration with DJI SDK and FlightHub 2 for mission management
- **Use Case:** Ideal for defense, inspection, mapping, and exploration scenarios

### Onboard Computing Options

For on-premises, edge AI processing, the following computers are suitable for mounting on the DJI M400:

| Model                     | Specs                                                 | Notes                                    |
|---------------------------|------------------------------------------------------|------------------------------------------|
| NVIDIA Jetson Nano        | Quad-core ARM Cortex-A57, 128-core Maxwell GPU, 4GB RAM | Entry-level, low power, basic AI tasks   |
| NVIDIA Jetson Xavier NX   | 6-core ARM v8.2, 384-core Volta GPU, 8GB RAM         | Mid-range, supports complex AI workloads |
| NVIDIA Jetson Orin Nano   | Up to 6-core ARM Cortex-A78AE, 1024-core Ampere GPU, 8GB RAM | High performance, advanced AI inference  |
| Raspberry Pi 5            | Quad-core ARM Cortex-A76, up to 8GB RAM              | Affordable, community support            |
| Khadas Edge2              | ARM Cortex-A76/A55, Mali-G610 GPU, up to 8GB RAM     | Compact, decent AI capability            |

These devices are commonly used for real-time AI inference, vision processing, and integration with ROS and SDKs for autonomous drone applications.

## STT (Speech-to-Text) Component

- **Short Analysis:**  
  The system supports multiple STT engines (Google Speech Recognition, Vosk, OpenAI Whisper) for Korean command transcription.
  - **Google Speech Recognition:** High accuracy, cloud-based, requires internet.
  - **Vosk:** Fast, fully offline, moderate accuracy.
  - **OpenAI Whisper:** Modern deep learning model, supports local execution, high accuracy, heavier resource use.

## LLM Component

### Fine-Tuning Methods

- **Supervised Fine-Tuning:** Train the model on a labeled, task-specific dataset.
- **Parameter-Efficient Fine-Tuning (PEFT):** Use techniques like LoRA/QLoRA for efficient adaptation.
- **Adapter-Based Fine-Tuning:** Insert small trainable modules (adapters) for minimal base model changes.
- **Instruction Fine-Tuning:** Use instruction-formatted datasets for command-following behavior.
- **Model Distillation:** Create smaller models for edge deployment.

### Recommended Korean LLM Candidates

| Model Name                     | Size     | Hugging Face Link                                                                 | Notes                                 |
|--------------------------------|----------|-----------------------------------------------------------------------------------|---------------------------------------|
| upskyy/e5-small-korean         | ~50M     | [Hugging Face](https://huggingface.co/upskyy/e5-small-korean)                     | Small, efficient, semantic tasks      |
| yanolja/EEVE-Korean-10.8B-v1.0 | 10.8B    | [Hugging Face](https://huggingface.co/yanolja/EEVE-Korean-10.8B-v1.0)             | Large, Korean-optimized               |
| KRAFTON/KORani-v3-13B          | 13B      | [Hugging Face](https://huggingface.co/KRAFTON/KORani-v3-13B)                      | LLaMA-based, dialogue fine-tuned      |
| Polyglot-Ko                    | 1.3B–12.8B | [Hugging Face](https://huggingface.co/collections/open-ko-llm-leaderboard/ko-llm-leaderboard-best-models-659c7e45a481ceea4c883506) | Multiple sizes, open source           |
| EXAONE-3-7.8B                  | 7.8B     | [Hugging Face](https://huggingface.co/lg-ai/exaone-3-7.8b)                        | Strong Korean/English performance     |

## Vision Encoder

- **YOLOv8 Integration:**  
  The system utilizes YOLOv8 as the vision encoder for real-time object detection and scene understanding. YOLOv8 is deployed on the onboard computer for efficient edge inference.

### Example Metadata Format

The vision encoder outputs metadata in a structured JSON format, such as:

```json
{
  "timestamp": "2025-07-14T14:22:00Z",
  "location": {"lat": 37.12345, "lon": 127.12345, "alt": 50},
  "objects": [
    {"type": "person", "confidence": 0.94, "bbox": [120, 80, 180, 200]},
    {"type": "vehicle", "confidence": 0.88, "bbox": [300, 150, 400, 250]}
  ],
  "image_id": "frame_000123"
}
```

This metadata is transmitted to the GCS and used by the LLM for automated mission reporting and situational awareness.

## Example Voice Commands

| Example Command                        | Description                                  |
|-----------------------------------------|----------------------------------------------|
| 이륙해.                                | Take off.                                    |
| 웨이포인트 A B C 정찰                  | Reconnaissance at waypoints A, B, and C.     |
| 고도 50미터 유지하면서 사람 찾아내      | Maintain 50m altitude and detect people.     |
| 착륙 지점으로 이동                      | Move to landing point.                       |
| 지정 구역을 순찰해                      | Patrol the designated area.                  |
| 차량을 추적해                          | Track the vehicle.                           |

## On-Premises Management Software

The system will utilize DJI's FlightHub 2 On-Premises packages for secure, scalable, and compliant drone fleet management:

| Package Name                                                        | Description                                  |
|---------------------------------------------------------------------|----------------------------------------------|
| FlightHub 2 On-Premises Version Device Expansion (1 Device)         | Add 1 device to on-premises management       |
| FlightHub 2 On-Premises Version Basic Package (1 Device)            | Basic on-premises management for 1 device    |
| FlightHub 2 On-Premises Version Upgraded Validity (1Year/1Device)   | 1-year validity extension for 1 device       |
| FlightHub 2 On-Premises Version Device Expansion (5 Devices)        | Add 5 devices to on-premises management      |

These packages enable full local control, data privacy, and compliance with defense requirements.

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
   - [YOLOv8 (Ultralytics)](https://github.com/ultralytics/ultralytics)

3. **Configure Models**
   - Download and set up Korean models for Vosk and Whisper.
   - Download YOLOv8 weights for object detection.
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

## Key References

- [TypeFly: Flying Drones with Large Language Model](https://arxiv.org/abs/2312.14950)
- [LLM-DaaS: LLM-driven Drone-as-a-Service Operations from Text User Requests](https://arxiv.org/abs/2412.11672)
- [ROS-LLM: A ROS framework for embodied AI with task feedback and structured reasoning](https://arxiv.org/abs/2406.19741)
- [LLM-Land: Large Language Models for Context-Aware Drone Landing](https://arxiv.org/abs/2505.06399)
- [UAV-VLA: Vision-Language-Action System for Large Scale Aerial Mission Generation](https://arxiv.org/abs/2501.05014)
- [KIT-19: Korean Instruction Dataset for LLM Fine-Tuning](https://arxiv.org/html/2403.16444v1)

## Contact
