# Transformers and “Attention Is All You Need”

## The paper and the PDF

The original paper is **“Attention Is All You Need”**, by Ashish Vaswani and collaborators, published in 2017. It introduced the Transformer architecture, which uses attention rather than recurrent or convolutional sequence processing as its central mechanism.

- [Paper abstract and HTML/PDF links on arXiv](https://arxiv.org/abs/1706.03762)
- [Direct PDF](https://arxiv.org/pdf/1706.03762)

The paper is linked here rather than copied into the repository. Read it alongside this beginner-oriented guide; the paper’s diagrams and equations are valuable once you know the main pieces.

## Why Transformers mattered

Earlier sequence models often processed tokens one after another. That made it harder to parallelize training and to connect information far apart in a sequence. A Transformer lets each token use attention to weigh information from other tokens, enabling more parallel training and flexible long-range relationships (subject to context length and compute limits).

## The original encoder-decoder Transformer

The paper describes a model for sequence-to-sequence tasks such as translation:

1. **Tokenization:** Convert text into token IDs. Tokens may be whole words, word pieces, or characters.
2. **Embeddings:** Map each token ID to a learned vector.
3. **Positional information:** Add position encodings so the model can distinguish token order. The original paper used sinusoidal encodings; learned positional methods are also common.
4. **Encoder stack:** Each layer contains multi-head self-attention and a position-wise feed-forward network, with residual connections and layer normalization.
5. **Decoder stack:** Each layer has masked self-attention, encoder-decoder attention, and a feed-forward network. The mask prevents a position from seeing future output tokens.
6. **Output projection and softmax:** Convert decoder states into probabilities for the next output token.

## Self-attention, step by step

For each input representation, learned projections produce a **query (Q)**, **key (K)**, and **value (V)**. Queries compare with keys to determine how much to attend to each position; the resulting weights mix the values.

Scaled dot-product attention is:

`Attention(Q, K, V) = softmax(QKᵀ / √dₖ) V`

- `QKᵀ` measures compatibility between queries and keys.
- Dividing by `√dₖ` keeps dot products from becoming too large as key dimensions grow.
- `softmax` turns scores into normalized weights.
- Multiplying by `V` forms a weighted combination of information.

In **self-attention**, Q, K, and V come from the same sequence. In **cross-attention**, decoder queries attend to encoder keys and values. In **causal/masked self-attention**, future-token scores are blocked so generation can proceed left to right.

## Multi-head attention

Instead of doing one attention calculation, the model uses several heads with separate learned projections. Heads can learn different relationships. Their outputs are concatenated and projected back into the model dimension.

## Other important parts

- **Feed-forward network (FFN):** A small neural network applied independently at each sequence position after attention.
- **Residual connections:** Add a layer’s input to its output, helping information and gradients flow through deep stacks.
- **Layer normalization:** Stabilizes activations during training.
- **Dropout:** Regularization used in the original model to reduce overfitting.
- **Autoregressive generation:** Predict a next token, append it, and repeat; decoding may use greedy selection, sampling, or beam search depending on the task.

## Encoder, decoder, and decoder-only models

- **Encoder-only** models build contextual representations and are commonly used for understanding tasks.
- **Encoder-decoder** models encode an input and generate an output conditioned on it, as in the original paper’s translation setup.
- **Decoder-only** models use causal attention to predict subsequent tokens and are widely used for text generation.

These are related Transformer designs, not interchangeable descriptions of one exact model. Modern architectures and training recipes vary.

## A beginner reading plan for the paper

1. Read the abstract and introduction; identify the problem the authors wanted to solve.
2. Study Figure 1 to see the encoder/decoder flow.
3. Read Section 3 and connect each attention equation to the plain-language steps above.
4. Inspect the positional encoding section and training setup.
5. Read the results and limitations critically; reported results reflect the datasets and methods available at the time.
6. Write down what the paper does not claim: attention is not human understanding, and the architecture alone does not guarantee factual or safe outputs.

## Try it yourself

- Draw one encoder layer and one decoder layer, labeling attention, FFN, residuals, and normalization.
- Implement scaled dot-product attention on tiny arrays and verify that attention weights sum to one along the attended positions.
- Change the mask in a toy example and observe why a language model must not see future target tokens during training.
- Compare model latency, memory, and quality for a small sequence-length change.

## Caveats

Attention has computational and memory costs that grow with sequence length in the standard form. Transformers can produce fluent but incorrect text, inherit data biases, expose sensitive information, and be vulnerable to misuse. Validate outputs and design appropriate safeguards for the application.
