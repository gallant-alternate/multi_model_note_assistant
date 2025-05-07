Sure! Here's the full `README.md` content formatted for direct copy-paste:

---


# multi_model_note_assistant

**multi_model_note_assistant** is a multimodal pipeline that converts lecture videos into high-quality structured notes using speech recognition, OCR, summarization, and clustering techniques.

## ✨ Features

- Slide extraction and deduplication
- Audio transcription via DeepSpeech, Vosk, Wav2Vec, etc.
- Structured slide + transcript alignment
- Extractive summarization (TextRank, LSA, etc.)
- Abstractive summarization using BART, Pegasus, etc.
- ChatGPT summarization support (optional)
- Full structured output with figures and aligned content
- GPU support for fast processing

## 🚀 Setup

### 1. Clone the Repository

```bash
git clone https://github.com/gallant-alternate/multi_model_note_assistant.git
cd multi_model_note_assistant
````

### 2. Create and Activate Conda Environment

#### Recommended: Fast setup using `.yml`

```bash
conda env create -f environment.yml
conda activate l2n
```

#### Manual Setup (Python 3.7)

```bash
conda create -n l2n python=3.7
conda activate l2n
pip install -r requirements.txt
```

> ⚠️ Note: Some libraries (e.g. `pattern`) only work with numpy < 1.26 and Python 3.7.

### 3. Install Required NLTK Data

```python
import nltk
nltk.download('punkt')
```

### 4. Prepare Models

* For DeepSpeech/Vosk, download model files and pass via `--transcribe_model_dir`
* HuggingFace models will auto-download on first use (internet required)

## 🛠️ Usage

Basic command:

```bash
python -m lecture2notes.end_to_end.main --auto_id -tm deepspeech \
--structured_joined_summarization_method abstractive \
--structured_joined_abs_summarizer sshleifer/distilbart-cnn-12-6 \
path/to/video.mp4
```

### Common Flags

* `--skip_to N` – resume pipeline from step `N`
* `--remove_duplicates` – deduplicate similar slides
* `--abs_hf_api` – use HuggingFace inference API (requires token)
* `--summarization_structured structured_joined` – enable structured output

## 📦 Output

The pipeline will create a subdirectory under `process/` containing:

* Extracted frames
* Audio transcript (`audio.json`)
* Slide structure (`slide-ssa.json`)
* Final summaries: `summarized.json`, `summarized.txt`

## ⚠️ Notes

* Python 3.7 is required for compatibility with `pattern` and some older packages
* GPU highly recommended for speed (especially for BART models)
* Ensure internet access for model auto-download unless pre-downloaded

## 📄 License

MIT License

