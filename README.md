# Chatterbox TTS Server — Windows Edition

**Maintainer:** [HunterIsLive](https://github.com/HunterisLive-1)

Self-hosted text-to-speech server built on [**Chatterbox**](https://github.com/resemble-ai/chatterbox) by [Resemble AI](https://www.resemble.ai/). This edition adds **multilingual synthesis**, a **browser UI**, **voice cloning**, **chunked / audiobook-scale generation**, and **streamlined Windows setup** (NVIDIA CUDA, AMD ROCm, or CPU).

**Repository:** [github.com/HunterisLive-1/Chatterbox-TTS-Server-windows-easyInstallation](https://github.com/HunterisLive-1/Chatterbox-TTS-Server-windows-easyInstallation)

---

## Highlights

- **24+ languages** — Arabic, Chinese, Danish, Dutch, English, Finnish, French, German, Greek, Hebrew, Hindi, Italian, Japanese, Korean, Malay, Norwegian, Polish, Portuguese, Russian, Spanish, Swedish, Swahili, Turkish, and more  
- **Voice cloning** — reference audio via Web UI (`./reference_audio`)  
- **Predefined voices** — drop `.wav` / `.mp3` in `./voices`  
- **Long-form text** — optional splitting with configurable chunk size  
- **Windows-friendly** — guided install (`easy-installation` / `install.bat` flow as documented in-repo)  
- **Acceleration** — NVIDIA (CUDA), AMD (ROCm), or CPU  
- **APIs** — FastAPI with `/docs`; includes an **OpenAI-compatible** speech endpoint  

---

## Requirements

- **OS:** Windows 10/11 (64-bit) or Linux  
- **Python:** 3.10+  
- **RAM:** 4 GB+ (8 GB+ recommended)  
- **Disk:** ~5 GB+ for models  
- **GPU (optional):** NVIDIA with 4 GB+ VRAM, or supported AMD (e.g. RX 6000/7000 series)  

---

## Quick start (Windows)

1. **Clone this repository**

   ```bash
   git clone https://github.com/HunterisLive-1/Chatterbox-TTS-Server-windows-easyInstallation.git
   cd Chatterbox-TTS-Server-windows-easyInstallation
   ```

2. **Install** — double-click **`setup.bat`** (runs `easy-installation/run-setup.ps1`) and follow the prompts for **NVIDIA**, **CPU**, or **AMD (ROCm)**.

3. **Run** — `win-run.bat` (from repo root, as shipped).

4. **Open** — [http://localhost:8004](http://localhost:8004)  
   API reference: [http://localhost:8004/docs](http://localhost:8004/docs)

---

## Manual install (Linux / advanced)

1. **Clone**

   ```bash
   git clone https://github.com/HunterisLive-1/Chatterbox-TTS-Server-windows-easyInstallation.git
   cd Chatterbox-TTS-Server-windows-easyInstallation
   ```

2. **Virtual environment** (Python 3.10 recommended)

   ```bash
   python3 -m venv venv
   source venv/bin/activate
   pip install --upgrade pip
   ```

3. **Dependencies** (pick one)

   ```bash
   pip install -r requirements-nvidia.txt   # NVIDIA
   pip install -r requirements-rocm.txt    # AMD ROCm
   pip install -r requirements.txt          # CPU
   ```

4. **Start**

   ```bash
   source venv/bin/activate
   python server.py
   ```

---

## Usage

### Web UI

1. Enter text and choose **language**  
2. Select **predefined** or **clone** voice mode  
3. Tune generation options as needed  
4. Generate and play / download audio  

### API examples

**TTS (illustrative JSON body):**

```json
POST /tts
{
  "text": "Hello world!",
  "language": "en",
  "voice_mode": "predefined",
  "temperature": 0.7,
  "speed_factor": 1.0
}
```

**OpenAI-compatible speech:**

```json
POST /v1/audio/speech
{
  "input": "Your text here",
  "voice": "S1",
  "language": "en",
  "response_format": "wav"
}
```

---

## Configuration

Edit `config.yaml` (defaults shown conceptually):

```yaml
server:
  host: "0.0.0.0"
  port: 8004

tts_engine:
  device: "auto"  # auto, cuda, cpu

generation_defaults:
  temperature: 0.7
  language: "en"
```

---

## Troubleshooting

- **GPU not visible** — install vendor drivers; restart; confirm `device` in config.  
- **Import / dependency errors** — activate the same venv you used to install requirements.  
- **Port in use** — change `server.port` in `config.yaml`.  

For bugs or feature requests, use **Issues** on [this repository](https://github.com/HunterisLive-1/Chatterbox-TTS-Server-windows-easyInstallation).

---

## Contributing

Pull requests and issues are welcome. Please keep changes focused and test on your target platform (Windows / Linux, CPU or GPU) when possible.

---

## License

MIT License — see `LICENSE` in the repository.

---

## Acknowledgements

- **[Resemble AI](https://www.resemble.ai/)** — [**Chatterbox TTS**](https://github.com/resemble-ai/chatterbox) model and ecosystem  

---

*Self-host Chatterbox-powered speech with a clean UI and flexible APIs.*
