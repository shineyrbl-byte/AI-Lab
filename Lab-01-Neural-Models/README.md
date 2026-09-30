# Lab 1 — Neural Models: Learning, Depth, Activations, and Output Layers

This laboratory explores how neural networks learn through backpropagation and gradient-based optimization, with a focus on nonlinear hidden layers, activation functions, initialization, and output layers.

## Problem

The main task uses the XOR problem:

| Input  | Output |
| ------ | -----: |
| (0, 0) |      0 |
| (0, 1) |      1 |
| (1, 0) |      1 |
| (1, 1) |      0 |

A single affine layer cannot represent XOR because the data is not linearly separable. A nonlinear hidden layer is therefore required.

## Model

The binary XOR classifier uses:

* Architecture: `2 → 2 → 1`
* Hidden activation: Sigmoid
* Output: logits during training
* Loss: `BCEWithLogitsLoss`
* Optimizer: SGD
* Full-batch training
* Random initialization

The laboratory also compares **Sigmoid, Tanh, and ReLU** as hidden-layer activation functions.

## Experiments

The notebook covers:

1. XOR problem specification and linear separability
2. Design of a `2 → 2 → 1` neural network
3. PyTorch implementation and training
4. Loss reduction and prediction checks
5. Backpropagation and first-layer gradients
6. Symmetry caused by zero initialization
7. Comparison of Sigmoid, Tanh, and ReLU
8. Extension from binary XOR to a three-class classification problem
9. Softmax probabilities and multiclass cross-entropy

## Key Results

The binary model successfully classified all four XOR examples:

* Initial loss: `0.7482`
* Final loss: `0.00263`
* Accuracy: `4/4`

Activation comparison:

| Hidden Activation | Final Loss | Correct |
| ----------------- | ---------: | ------: |
| Sigmoid           |   0.002630 |     4/4 |
| Tanh              |   0.000637 |     4/4 |
| ReLU              |   0.346600 |     3/4 |

The three-class extension also correctly classified all four examples:

`[0, 1, 1, 2]`

## LLM Usage

One LLM prompt was used to generate the initial PyTorch implementation.

The generated implementation was then manually checked against the laboratory requirements. Two implementation decisions were documented:

1. `BCEWithLogitsLoss` was used with raw output logits for numerical stability.
2. `sigmoid` was applied after training to obtain probabilities for interpretation and threshold-based predictions.

The architecture, dataset, and experimental requirements were kept unchanged.

## Files

* `Lab1_Neural_Models.ipynb` — Complete Colab/Jupyter notebook containing code, outputs, experiments, and explanations.
* `Lab1_Neural_Models_Report.pdf` — Short report containing the problem specification, model design, LLM prompt, results, and reflections.
