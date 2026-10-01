# Transformers Hands-On Lab

This repo contains my work for the Transformers lab. It demonstrates the three
Transformer families and compares a locally run LLM (Mistral via Ollama) with a
hosted assistant (Claude).

## Background

The Transformer was introduced for **machine translation**: take one sequence in
(English), produce another out (French). Today's models use one or both halves of
the original architecture:

| Type | Example | Typical uses | Demo in this repo |
|---|---|---|---|
| Encoder-decoder | T5, BERT2BERT | Translation, sequence-to-sequence tasks | Section 1 |
| Decoder-only | GPT-2, GPT-style models | Text generation, chatbots, code, summarization | Section 2 |
| Encoder-only | BERT, DistilBERT | Sentiment analysis, semantic search, retrieval, clustering | Section 3 |

Key concepts covered: attention, self-attention, cross-attention, multi-head
attention, positional encoding, and masked attention.

## Repository contents

- `transformers_lab.ipynb` - main notebook with code, outputs and observations
- `requirements.txt` - Python dependencies
- `README.md` - this file

## Setup

### Option A: Google Colab (what I used)

1. Upload `transformers_lab.ipynb` to https://colab.research.google.com
2. Set **Runtime -> Change runtime type -> T4 GPU** (optional but faster).
3. Run the cells in order. The first cell installs the Python packages.
4. Before the Ollama section, run these two cells to install and start Ollama:
   ```python
   !apt-get install -y zstd > /dev/null 2>&1
   !curl -fsSL https://ollama.com/install.sh | sh
   ```
   ```python
   import subprocess, time
   subprocess.Popen(["ollama", "serve"])
   time.sleep(5)
   !ollama pull mistral
   ```

### Option B: Run locally

```bash
python -m venv venv
source venv/bin/activate          # Windows: venv\Scripts\activate
pip install -r requirements.txt
```

Install Ollama from https://ollama.com/download, then:

```bash
ollama serve                      # skip if it already runs as a service
ollama pull mistral
jupyter notebook transformers_lab.ipynb
```

The first run downloads model weights from Hugging Face (several GB in total), so
internet access and disk space are needed.

## What each section does

1. **Encoder-decoder** - English->German with `google/bert2bert_L-24_wmt_en_de`,
   English->French with `google-t5/t5-base`, English->Hinglish with
   `rvv-karma/English2Hinglish-Flan-T5-Base`.
2. **Decoder-only** - next-token text generation with GPT-2.
3. **Encoder-only** - sentiment analysis with DistilBERT fine-tuned on SST-2.
4. **Ollama vs. hosted model** - four prompts sent to local Mistral and to Claude,
   with a side-by-side comparison table.

## Results and observations

- **Translation:** BERT2BERT (English->German) gave a fluent, accurate sentence and
  was the best. T5 (English->French) translated "I love machine learning" as
  "J'aime l'apprentissage par machine", which is understandable but literal (the
  standard term is "apprentissage automatique"). The Hinglish model was the weakest:
  its output, "Life crazy haiNot me", was garbled, because it is a small fine-tune.
- **GPT-2 generation:** The text was fluent but vague, and it stopped mid-sentence at
  the 30-token limit. This matches masked self-attention: each token is predicted
  from the tokens before it.
- **Sentiment analysis:** Clear positive and negative sentences were classified
  correctly with ~0.99+ confidence. The neutral sentence "The product arrived on
  Tuesday." was labelled POSITIVE (0.94) because the model was trained on binary
  movie-review data and has no neutral class.
- **Ollama vs. Claude:** Mistral solved the math problem correctly but ignored length
  limits, invented a plot detail, and wrote a palindrome function with a bug (it
  returns `False` for "abba"). Claude followed the instructions and was more
  accurate. Ollama found no GPU on Colab, so Mistral ran on CPU and was slow.

## Notes

- Small local models are cheaper and private, but noticeably less reliable than
  large hosted models, especially on code and strict instructions.
- Warnings printed during model loading (unauthenticated HF Hub requests, deprecated
  generation arguments, tied-weights notice) did not stop the notebook from running.
