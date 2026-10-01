# Building and Learning a Bayesian Network

Lab on the binary Sprinkler Bayesian network, using pgmpy and a local coding
LLM (Qwen2.5-Coder-1.5B-Instruct) as an engineering assistant.

Network: Cloudy -> Rain, Cloudy -> Sprinkler, Rain -> WetGrass, Sprinkler -> WetGrass.

## What the notebook covers

1. Building the network with explicit CPTs and validating it with `check_model()`.
2. Exact inference with variable elimination for P(Rain=1 | WetGrass=1) = 0.705,
   verified independently by enumerating all 16 assignments.
3. Generating synthetic data and estimating CPTs by maximum likelihood.
4. Sparse data: comparing MLE with Bayesian (BDeu) estimation at N=30.
5. Asking the LLM to write pgmpy code, then inspecting and validating it
   before running anything.
6. Homework: LLM-generated code for three new queries, with predictions.
7. Classroom exercises: LLM explanation of the WetGrass CPT, and why estimates
   vary across random seeds.

## My findings

- Homework queries: P(S=1 | W=1) = 0.428, P(C=1 | W=1) = 0.575, and
  P(R=1 | W=1, S=0) = 0.992. All three moved in the direction I predicted
  (the last one is explaining away).
- The LLM-generated programs were wrong, even though the basic AST safety
  check passed them. They used the obsolete `BayesianModel`, reversed the
  Rain CPD, wrote CPDs whose columns do not sum to 1, and did not use
  `VariableElimination`. I did not execute them.
- The LLM's explanation of the WetGrass CPT columns was incorrect. It mixed up
  rows and columns and invented probabilities.
- Estimates of P(R=1 | C=1) varied across seeds (0.694 to 0.796 at N=100)
  because of sampling variability, not tool inconsistency. The LLM's
  explanation of this was mostly wrong.
- Main lesson: code that runs is not the same as a correct model, so generated
  code needs inspection and validation against a trusted reference.

## How to run

```
pip install -r requirements.txt
```

Open `llm_bn.ipynb` (Google Colab with a GPU runtime is recommended) and run
it from top to bottom. The first LLM cell downloads about 3 GB of model
weights.
