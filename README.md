# LLM-Enabled Drone GCS  
_A Ground Control Station Project with Integrated STT, LLM, and Vision Metadata for Defense Applications_

## Project Overview

This repository details the development of a next-generation Ground Control Station (GCS) for drones, integrating **Speech-to-Text (STT)**, **Large Language Models (LLM)**, and **vision-based metadata processing**. The system is engineered for **defense applications**, prioritizing secure, robust, and intelligent drone operations through natural language commands and automated mission reporting.

## System Architecture

### End-to-End Workflow

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

- **Type:** Enterprise-grade quadcopter
- **Flight Time:** Up to 59 minutes
- **Payload Capacity:** Up to 6 kg
- **Sensors:** LiDAR, mmWave radar, fisheye vision, RTK positioning
- **Video Transmission:** Up to 40 km with O4 Enterprise Enhanced Video Transmission
- **Multi-Payload:** Supports up to 7 simultaneous payloads
- **Obstacle Avoidance:** Advanced, including power-line and terrain detection
- **Use Cases:** Defense, inspection, mapping, search & rescue, exploration[1][2][3]

### Onboard Computing Options

| Model                   | CPU/GPU Specs                                             | AI Performance | Notable Features                |
|-------------------------|----------------------------------------------------------|----------------|----------------------------------|
| NVIDIA Jetson Nano      | Quad-core ARM Cortex-A57, 128-core Maxwell GPU, 4GB RAM  | 472 GFLOPS     | Entry-level, low power           |
| Jetson Xavier NX        | 6-core ARM v8.2, 384-core Volta GPU, 8GB RAM             | 21 TOPS        | Multi-sensor, strong AI support  |
| Jetson Orin Nano        | 6-core Cortex-A78AE, up to 1024-core Ampere GPU, 8GB RAM | 40 TOPS        | High performance, compact        |
| Raspberry Pi 5          | Quad-core Cortex-A76, up to 8GB RAM                      | -              | Affordable, broad community      |
| Khadas Edge2            | 8-core RK3588S, Mali-G610 GPU, up to 16GB RAM            | 6 TOPS         | 8K video, Wi-Fi 6, AI-ready      |[4][5][6][7][8][9][10][11][12][13]

## STT (Speech-to-Text) Component

- **Google Speech Recognition:**  
  High accuracy, cloud-based, requires internet.
- **Vosk:**  
  Fast, fully offline, moderate accuracy.
- **OpenAI Whisper:**  
  Deep learning, local execution, high accuracy, higher resource use.

## LLM Component

### Fine-Tuning Methods

- **Supervised Fine-Tuning:** Labeled, task-specific dataset adaptation.
- **Parameter-Efficient Fine-Tuning (PEFT):** LoRA/QLoRA for efficient updates.
- **Adapter-Based:** Small trainable modules for minimal base model changes.
- **Instruction Fine-Tuning:** Teach command-following using instruction datasets.
- **Model Distillation:** Smaller, efficient models for edge deployment.

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
  Real-time object detection, multi-scale, lightweight, and efficient for edge inference.  
  Outputs structured metadata for mission reporting and situational awareness[14][15].

#### Example Metadata Format

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

## Example Voice Command to SDK Command Mapping

| Example Command                        | LLM Output (Structured)         | DJI SDK/ROS Command Example              | Description                           |
|-----------------------------------------|----------------------------------|------------------------------------------|---------------------------------------|
| 이륙해.                                | CMD: TAKEOFF                    | `monitoredTakeoff()`                     | Take off                              |
| 웨이포인트 A B C 정찰                  | CMD: GOTO_WAYPOINTS A,B,C       | `goToWaypoint('A')`, ...                 | Recon at waypoints A, B, C            |
| 고도 50미터 유지하면서 사람 찾아내      | CMD: HOLD_ALT 50; DETECT PERSON | `holdAltitude(50)`, `detectObject('person')` | Maintain 50m, detect person           |
| 착륙 지점으로 이동                      | CMD: GOTO_LANDPOINT             | `goToLandPoint()`                        | Move to landing point                 |
| 지정 구역을 순찰해                      | CMD: PATROL AREA                | `patrolArea(area_id)`                     | Patrol designated area                |
| 차량을 추적해                          | CMD: TRACK VEHICLE              | `trackObject('vehicle')`                  | Track the vehicle                     |

## On-Premises Management Software

The system leverages **DJI FlightHub 2 On-Premises** for secure, scalable fleet management:

| Package Name                                                        | Description                                  |
|---------------------------------------------------------------------|----------------------------------------------|
| FlightHub 2 On-Premises Version Device Expansion (1 Device)         | Add 1 device to on-premises management       |
| FlightHub 2 On-Premises Version Basic Package (1 Device)            | Basic on-premises management for 1 device    |
| FlightHub 2 On-Premises Version Upgraded Validity (1Year/1Device)   | 1-year validity extension for 1 device       |
| FlightHub 2 On-Premises Version Device Expansion (5 Devices)        | Add 5 devices to on-premises management      |

- **Key Features:**  
  - OpenAPI for secondary development
  - MQTT Bridge for efficient, secure message delivery
  - Modular frontend components for rapid integration[16]

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
   - Download/setup Korean models for Vosk and Whisper
   - Download YOLOv8 weights
   - Ensure ffmpeg is in your PATH

4. **Run Example Code**
   - See `/stt/`, `/llm/`, `/vision/` directories for scripts and usage

## Defense-Oriented Design

- **Mission-Critical Reliability:**  
  All modules are validated in operational scenarios for robustness.
- **Offline and Secure Operation:**  
  Local execution ensures privacy and compliance.
- **Scalable and Modular:**  
  Adaptable for various drone platforms and mission profiles.

## Key References

- [TypeFly: Flying Drones with Large Language Model](https://arxiv.org/abs/2312.14950)
- [LLM-DaaS: LLM-driven Drone-as-a-Service Operations from Text User Requests](https://arxiv.org/abs/2412.11672)
- [ROS-LLM: A ROS framework for embodied AI with task feedback and structured reasoning](https://arxiv.org/abs/2406.19741)
- [LLM-Land: Large Language Models for Context-Aware Drone Landing](https://arxiv.org/abs/2505.06399)
- [UAV-VLA: Vision-Language-Action System for Large Scale Aerial Mission Generation](https://arxiv.org/abs/2501.05014)
- [KIT-19: Korean Instruction Dataset for LLM Fine-Tuning](https://arxiv.org/html/2403.16444v1)

## Contact

For collaboration or questions, please contact the maintainer at `your.email@domain.com`.

[1] https://enterprise.dji.com/matrice-400
[2] https://www.dji.com/media-center/announcements/dji-release-matrice-400
[3] https://hp-drones.com/en/dji-matrice-400-power-precision-and-efficiency-at-the-peak-of-drone-technology/
[4] https://www.nvidia.com/en-us/autonomous-machines/embedded-systems/jetson-nano/product-development/
[5] https://www.waveshare.com/jetson-xavier-nx.htm
[6] https://connecttech.com/product/nvidia-jetson-orin-nano-4gb-module/
[7] https://thepihut.com/products/raspberry-pi-5
[8] https://techexplorations.com/blog/review/khadas-edge2-an-ai-ready-single-board-computer-powerhouse
[9] https://www.macnica.co.jp/en/business/semiconductor/manufacturers/nvidia/products/134045/
[10] https://www.macnica.co.jp/en/business/semiconductor/manufacturers/nvidia/products/134047/
[11] https://crg.co.il/catalog/jetson-orin-nano-series-4gb-8gb/
[12] https://www.waveshare.com/raspberry-pi-5.htm
[13] https://www.khadas.com/edge2
[14] https://encord.com/blog/yolo-object-detection-guide/
[15] https://docs.ultralytics.com/ko/tasks/detect/
[16] https://enterprise-insights.dji.com/blog/dji-flighthub-2-on-premises-officially-released
[17] https://enterprise.dji.com/matrice-400/specs
[18] https://enterprise.dji.com/kr/matrice-400/specs
[19] https://www.youtube.com/watch?v=Cc7UMhmshpI
[20] https://www.heliguy.com/blogs/posts/dji-flighthub-2-on-premises-enhanced-drone-data-security/
