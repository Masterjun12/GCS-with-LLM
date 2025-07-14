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
[Vision Encoder]
      ↓
[Metadata Transmission]
      ↓
[LLM Report Generation]
```

## STT (Speech-to-Text) Component

- **Short Analysis:**  
  The system supports multiple STT engines (Google Speech Recognition, Vosk, OpenAI Whisper) for Korean command transcription.  
  - **Google Speech Recognition:** High accuracy, cloud-based, requires internet.  
  - **Vosk:** Fast, fully offline, moderate accuracy.  
  - **OpenAI Whisper:** Modern deep learning model, supports local execution, high accuracy, heavier resource use.

## LLM Component

### Fine-Tuning Methods

- **Supervised Fine-Tuning:**  
  Train the model on a labeled, task-specific dataset to adapt it to new tasks or domains[1][2].
- **Parameter-Efficient Fine-Tuning (PEFT):**  
  Techniques like LoRA/QLoRA update only a small subset of parameters, reducing hardware requirements and cost[2][3][4].
- **Adapter-Based Fine-Tuning:**  
  Insert small trainable modules (adapters) into the model, enabling efficient adaptation with minimal changes to the base model[2].
- **Instruction Fine-Tuning:**  
  Use instruction-formatted datasets to teach the model to follow specific user commands or prompts[3][5].
- **Model Distillation:**  
  Train a smaller model to mimic a larger one, useful for deploying on resource-constrained devices[2].

### Best Practices

- Start with a smaller model for faster iteration and lower compute cost[3].
- Use high-quality, domain-relevant datasets.
- Tune hyperparameters (learning rate, batch size, epochs) carefully to avoid overfitting or catastrophic forgetting[6].

## Recommended Korean LLM Candidates

| Model Name | Size | Hugging Face Link | Notes |
|------------|------|-------------------|-------|
| **upskyy/e5-small-korean** | ~50M | [Hugging Face](https://huggingface.co/upskyy/e5-small-korean) | Small, sentence transformer, good for semantic tasks[7] |
| **yanolja/EEVE-Korean-10.8B-v1.0** | 10.8B | [Hugging Face](https://huggingface.co/yanolja/EEVE-Korean-10.8B-v1.0) | Efficient Korean vocabulary extension, partial fine-tuning possible[8] |
| **KRAFTON/KORani-v3-13B** | 13B | [Hugging Face](https://huggingface.co/KRAFTON/KORani-v3-13B) | LLaMA-based, fine-tuned for Korean dialogue |
| **Polyglot-Ko** | 1.3B–12.8B | [Hugging Face](https://huggingface.co/collections/open-ko-llm-leaderboard/ko-llm-leaderboard-best-models-659c7e45a481ceea4c883506) | Multiple sizes, Korean-specific, open source[9][10] |
| **EXAONE-3-7.8B** | 7.8B | [Hugging Face](https://huggingface.co/lg-ai/exaone-3-7.8b) | Strong Korean/English performance[9] |

## Example Images

- **System Architecture**
- **STT Workflow**
- **Vision Encoder Output**

## Experimental Results

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

## Key References

- [TypeFly: Flying Drones with Large Language Model](https://arxiv.org/abs/2312.14950)[11][12]
- [LLM-DaaS: LLM-driven Drone-as-a-Service Operations from Text User Requests](https://arxiv.org/abs/2412.11672)
- [ROS-LLM: A ROS framework for embodied AI with task feedback and structured reasoning](https://arxiv.org/abs/2406.19741)
- [LLM-Land: Large Language Models for Context-Aware Drone Landing](https://arxiv.org/abs/2505.06399)
- [UAV-VLA: Vision-Language-Action System for Large Scale Aerial Mission Generation](https://arxiv.org/abs/2501.05014)
- [KIT-19: Korean Instruction Dataset for LLM Fine-Tuning](https://arxiv.org/html/2403.16444v1)[5]

## Contact

For collaboration or questions, please contact the maintainer at `oylim98@gmail.com`.

[1] https://www.turing.com/resources/finetuning-large-language-models
[2] https://labelyourdata.com/articles/llm-fine-tuning/llm-fine-tuning-methods
[3] https://www.acorn.io/resources/learning-center/fine-tuning-llm/
[4] https://elice.io/en/newsroom/llama3.1-ko-benchmark
[5] https://typefly.github.io
[6] https://arxiv.org/abs/2410.17602
[7] https://huggingface.co/upskyy/e5-small-korean
[8] https://huggingface.co/yanolja/EEVE-Korean-10.8B-v1.0
[9] https://developers.google.com/machine-learning/crash-course/llm/tuning
[10] https://cohere.com/blog/fine-tuning
[11] https://huggingface.co/blog/amphora/navigating-ko-llm-research-1
[12] https://huggingface.co/KRAFTON/KORani-v3-13B
[13] https://arxiv.org/abs/2312.14950
[14] https://www.superannotate.com/blog/llm-fine-tuning
[15] https://www.datacamp.com/tutorial/fine-tuning-large-language-models
[16] https://arxiv.org/html/2408.13296v1
[17] https://github.com/enlipleai/kor_pretrain_LM
[18] https://myscale.com/blog/mastering-large-language-models-drone-control-autonomous-vehicles/
[19] https://huggingface.co/collections/open-ko-llm-leaderboard/ko-llm-leaderboard-best-models-659c7e45a481ceea4c883506
[20] https://arxiv.org/html/2403.16444v1
