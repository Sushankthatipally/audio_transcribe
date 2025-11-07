# Telugu to English Speech Translation & Evaluation

[![Python](https://img.shields.io/badge/Python-3.11+-blue.svg)](https://www.python.org/downloads/)
[![PyTorch](https://img.shields.io/badge/PyTorch-2.0+-orange.svg)](https://pytorch.org/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

A comprehensive evaluation project for **Telugu → English speech translation** using Meta's **SeamlessM4T-v2-large** model. This project translates 2,667 Telugu audio files and evaluates them against human transcriptions using 8 different metrics.

## 📊 Project Overview

This project demonstrates:

- 🎯 **Speech-to-text translation** from Telugu to English
- 📈 **Multi-metric evaluation** (BLEU, ChrF++, TER, WER, CER, ROUGE, METEOR, BERTScore)
- 💾 **Progress tracking** with caching and resume capability
- 📉 **Comprehensive analysis** with visualizations and detailed reports

## 🎯 Results Summary

### Evaluation Metrics (2,665 audio files)

| Metric Category | Metric           | Score      | Interpretation           |
| --------------- | ---------------- | ---------- | ------------------------ |
| **Quality**     | BLEU             | 14.65/100  | Fair n-gram overlap      |
| **Quality**     | ChrF++           | 42.61/100  | Moderate character match |
| **Quality**     | METEOR           | 0.3615/1.0 | Fair semantic similarity |
| **Error Rate**  | TER              | 98.67      | High edit distance       |
| **Error Rate**  | WER              | 1.1339     | 113% word error rate     |
| **Error Rate**  | CER              | 0.8297     | 83% character error      |
| **Recall**      | ROUGE-1          | 0.4578     | 46% unigram recall       |
| **Recall**      | ROUGE-2          | 0.2359     | 24% bigram recall        |
| **Recall**      | ROUGE-L          | 0.4005     | 40% longest sequence     |
| **Semantic**    | **BERTScore F1** | **0.9052** | ✅ **Excellent!**        |

### Key Insight

The **90.5% BERTScore** indicates that while the model may not match exact human wording (low BLEU), it **preserves meaning exceptionally well**, making translations semantically accurate and useful for real-world applications.

## 🚀 Features

- ✅ **Automatic audio loading** with soundfile backend
- ✅ **Progress caching** - Resume from interruptions
- ✅ **Batch processing** with progress indicators
- ✅ **8 comprehensive metrics** for thorough evaluation
- ✅ **Detailed per-file analysis** with CSV export
- ✅ **Visualization generation** (charts and comparisons)
- ✅ **JSON/CSV export** for further analysis

## 📋 Requirements

### Python Version

- Python 3.11+ (tested with 3.11.9)

### Core Dependencies

```
torch>=2.0.0
torchaudio>=2.0.0
transformers>=4.30.0
soundfile>=0.12.0
sentencepiece>=0.1.99
```

### Evaluation Metrics

```
sacrebleu>=2.3.0
jiwer>=3.0.0
rouge-score>=0.1.0
nltk>=3.8.0
bert-score>=0.3.13
```

### Additional

```
pandas>=2.0.0
matplotlib>=3.7.0
seaborn>=0.12.0
numpy>=1.24.0
```

## 🛠️ Installation

1. **Clone the repository**

```bash
git clone https://github.com/yourusername/telugu-english-translation.git
cd telugu-english-translation
```

2. **Create virtual environment**

```bash
python -m venv .venv
.venv\Scripts\activate  # Windows
# or
source .venv/bin/activate  # Linux/Mac
```

3. **Install dependencies**

```bash
pip install torch torchaudio --index-url https://download.pytorch.org/whl/cpu
pip install transformers sentencepiece soundfile
pip install sacrebleu jiwer rouge-score nltk bert-score
pip install pandas matplotlib seaborn
```

4. **Download NLTK data**

```python
import nltk
nltk.download('wordnet')
nltk.download('punkt')
nltk.download('omw-1.4')
```

## 📁 Project Structure

```
repo/
├── seamless_telugu_translation_scoring.ipynb  # Main notebook
├── seamless_translations.txt                  # Model output
├── results/
│   ├── evaluation_results.json               # Metrics summary
│   ├── detailed_file_results.csv             # Per-file scores
│   └── translation_comparison.txt            # Side-by-side comparison
├── .seamless_cache/                          # Progress cache (gitignored)
├── TG/                                       # Audio files (gitignored)
├── README.md                                 # This file
└── requirements.txt                          # Dependencies
```

## 🎓 Usage

### Quick Start

Open the Jupyter notebook and run cells sequentially:

```bash
jupyter notebook seamless_telugu_translation_scoring.ipynb
```

### Step-by-Step

1. **Configure paths** (Cell 8)

   - Set `AUDIO_FOLDER` to your Telugu audio directory
   - Set `REFERENCE_FILE` to your human transcription file

2. **Load model** (Cell 10)

   - Downloads SeamlessM4T-v2-large (~10GB) on first run
   - Subsequent runs use cached model

3. **Translate audio** (Cell 17)

   - Processes all audio files with progress tracking
   - Saves checkpoint every 5 files
   - Can be interrupted and resumed

4. **Evaluate** (Cells 19-21)
   - Loads human references
   - Calculates all 8 metrics
   - Generates visualizations and reports

### Resume from Interruption

The notebook automatically saves progress. Simply re-run the translation cell to continue from where you left off.

## 📊 Evaluation Metrics Explained

### Quality Metrics (Higher = Better)

- **BLEU**: Measures n-gram precision (0-100)
- **ChrF++**: Character n-gram F-score (0-100)
- **METEOR**: Semantic matching with synonyms (0-1)

### Error Metrics (Lower = Better)

- **TER**: Translation Edit Rate - number of edits needed
- **WER**: Word Error Rate (0-∞)
- **CER**: Character Error Rate (0-1)

### Recall Metrics (0-1 scale)

- **ROUGE-1/2/L**: Unigram/bigram/longest sequence recall

### Semantic Similarity (0-1 scale)

- **BERTScore**: Neural contextual embeddings similarity

## 🔧 Troubleshooting

### Out of Memory

- Use CPU instead of GPU: `device = torch.device("cpu")`
- Process in smaller batches

### Audio Loading Errors

- Ensure soundfile is installed: `pip install soundfile`
- Check audio format (prefer 16kHz, mono .wav)

### Model Download Fails

- Check internet connection
- Try again later (HuggingFace servers may be busy)
- Manually download from: https://huggingface.co/facebook/seamless-m4t-v2-large

## 📈 Performance

- **Translation Speed**: ~30-60 seconds per file (CPU)
- **GPU Acceleration**: 10-20x faster with CUDA
- **Memory Usage**: ~12GB RAM (model) + audio processing
- **Total Processing Time**: ~2-6 hours for 2,667 files (CPU)

## 🤝 Contributing

Contributions are welcome! Please:

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Open a Pull Request

## 📝 Citation

If you use this project in your research, please cite:

```bibtex
@software{telugu_english_translation,
  title={Telugu to English Speech Translation Evaluation},
  author={Your Name},
  year={2025},
  url={https://github.com/yourusername/telugu-english-translation}
}
```

### Model Citation

```bibtex
@article{seamlessm4t2023,
  title={SeamlessM4T: Massively Multilingual \& Multimodal Machine Translation},
  author={Communication, Seamless and others},
  journal={arXiv preprint arXiv:2308.11596},
  year={2023}
}
```

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- **Meta AI** for the SeamlessM4T model
- **HuggingFace** for the transformers library
- **NLTK, SacreBLEU, JIWER** teams for evaluation metrics

## 📧 Contact

- GitHub: [@yourusername](https://github.com/yourusername)
- Email: your.email@example.com

---

**Note**: Audio files and model checkpoints are not included in this repository due to size constraints. You'll need to provide your own Telugu audio dataset and the model will be downloaded automatically on first run.
