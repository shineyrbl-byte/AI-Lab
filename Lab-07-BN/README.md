# Lab 5 — Building and Learning an Autoregressive Language Model

This laboratory explores the connection between Bayesian networks,
probabilistic modelling, and autoregressive language models.

## Topics Covered

- First-order autoregressive language model
- Conditional probability tables (CPTs)
- Transition-count estimation
- Probability normalization
- Greedy and sampling-based text generation
- Second-order autoregressive language model
- Comparison of first-order and second-order models
- Connection between simple probabilistic models and modern language models
- LLM-assisted implementation and independent validation

## Models

The first-order model estimates:

P(X_t | X_(t-1))

The second-order model estimates:

P(X_t | X_(t-2), X_(t-1))

The models are implemented using ordinary Python data structures and
probability calculations rather than pretrained language models.

## Results

The implemented models were tested by checking that conditional
probability distributions sum to approximately 1.

The observed model sizes were:

| Model | Contexts | Probability Entries |
|---|---:|---:|
| First-order | 11 | 17 |
| Second-order | 14 | 18 |

The notebook also contains examples of generated text using both greedy
and sampling-based generation.

## LLM-Assisted Development

An LLM was used as a coding assistant to implement and modify the
language models from explicit probabilistic specifications.

The generated code was inspected and independently tested.

One issue was found in the second-order generation code: the initial
implementation started generation with the unseen context
`(<START>, <START>)`, causing empty generated sentences.

The generation logic was corrected so that the first word is selected
after `<START>` and the second-order model is then used with the
appropriate two-token context.

## Files

- `llm_language_model.ipynb` — Complete laboratory notebook
- `requirements.txt` — Python dependencies

## How to Run

Open `llm_language_model.ipynb` in Google Colab and run the cells from
top to bottom.
