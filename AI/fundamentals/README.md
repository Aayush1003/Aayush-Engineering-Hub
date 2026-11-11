# AI Foundations and Learning Path

This path assumes you are learning from the beginning. You do not need to master every mathematical detail before building small projects; learn concepts, implement them, and revisit the math as needed.

## 0. Tools and programming

- Python: functions, classes, modules, virtual environments, exceptions, and type hints.
- NumPy for arrays and vectorized computation; pandas for tabular data; Matplotlib for plots.
- Git and command-line basics; Jupyter notebooks for exploration, ordinary Python modules for reusable code.
- Practice: load a small public dataset, inspect it, plot it, and write a short script that reproduces your analysis.

## 1. Essential math

- **Linear algebra:** vectors, matrices, dot products, matrix multiplication, norms, and dimensions/shapes.
- **Probability and statistics:** distributions, mean/variance, conditional probability, sampling, and uncertainty.
- **Calculus:** derivatives, gradients, chain rule, and the intuition behind gradient descent.
- Practice: calculate a linear model’s predictions and mean-squared error with NumPy, then update its parameters using gradients.

## 2. Machine learning basics

- Features and labels; train/validation/test splits; data leakage.
- Regression and classification; linear/logistic regression; decision trees and nearest neighbors.
- Loss functions, optimization, regularization, and overfitting/underfitting.
- Metrics: accuracy, precision, recall, F1, ROC-AUC (when appropriate), and task-specific costs.
- Practice: build a baseline classifier; compare it with a simple alternative and explain errors, not just the headline score.

## 3. Neural networks

- Neurons, layers, activations, forward pass, loss, backpropagation, and gradient descent.
- Batches, epochs, learning rates, initialization, regularization, and validation.
- Use a framework such as PyTorch after you understand the shape and flow of a small model.
- Practice: train a small neural network on a well-known educational dataset and log its configuration and metrics.

## 4. Choose a specialization

- **Computer vision:** image classification, convolution, augmentation, detection, and segmentation.
- **Language and NLP:** tokenization, embeddings, sequence models, attention, Transformers, and language-model evaluation.
- **Recommenders:** candidate generation, ranking, feedback loops, and offline/online evaluation.
- **Reinforcement learning:** states, actions, rewards, policies, and safe evaluation in a controlled environment.

## 5. Modern generative AI

- Tokenization, embeddings, pretraining, fine-tuning, prompting, and inference.
- Retrieval-augmented generation (RAG): chunking, embeddings, retrieval, citations, and retrieval evaluation.
- Model limitations: hallucinations, bias, privacy risks, prompt injection, and changing behavior across versions.
- Practice: build a small document-question-answering demo over non-sensitive documents and test whether answers are grounded in retrieved sources.

## 6. AI engineering habits

- Start with a baseline and measurable requirements. Keep a held-out evaluation set.
- Version code, configuration, and data references; never commit secrets or private datasets.
- Track experiments, random seeds, model versions, latency, memory, and cost.
- Add automated tests for preprocessing and interfaces; test model quality with a representative evaluation set.
- Review privacy, licensing, fairness, accessibility, and safety for the intended application.

## Checkpoints

- [ ] Explain the difference between training, validation, and test data.
- [ ] Train and evaluate a baseline without data leakage.
- [ ] Explain overfitting and use at least one method to reduce it.
- [ ] Read the [Transformer guide](../transformers/README.md) and summarize self-attention in your own words.
- [ ] Complete one small project with reproducible instructions, tests, evaluation results, and known limitations.
