# Infix to Postfix Translation with Transformers

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![TensorFlow](https://img.shields.io/badge/TensorFlow-2.x-orange.svg)
![Keras](https://img.shields.io/badge/Keras-Custom_Layers-red.svg)
![Deep Learning](https://img.shields.io/badge/Deep_Learning-NLP-success.svg)

> **Academic Context:** This project was developed as part of a university exam. It focuses on solving a recursive parsing problem using a custom-built Transformer architecture and comparing different training strategies.

## 📌 Problem Analysis & Mathematical Context
The objective of this project is to learn the algorithmic translation of arithmetic expressions from **Infix notation** (e.g., `(a+b)*c`) to **Postfix notation** (also known as Reverse Polish Notation, e.g., `ab+c*`).

This is not a simple sequence-to-sequence mapping task, but a complex **recursive parsing problem**:
* **Infix** requires complex precedence rules and parentheses to define scope.
* **Postfix** is unambiguous and stack-based, completely eliminating the need for parentheses.

Traditional Recurrent Neural Networks (RNNs/LSTMs) process data sequentially and struggle with this task. The transition to higher syntactic depths (e.g., Depth 4: `((a+b)*(c+d))`) forces the model to maintain a deep internal "stack" state across long intervening sequences, where RNNs typically fail due to the **Vanishing Gradient** problem.

## 🧠 Proposed Solution: The Custom Transformer
To overcome the limitations of RNNs, I implemented an **Encoder-Decoder Transformer** architecture entirely from scratch using TensorFlow/Keras. 

By leveraging the **Self-Attention** mechanism, the model is capable of direct parallel connections between any two symbols in the sequence, allowing it to easily learn structural dependencies (like matching deep parentheses) regardless of the distance between them.

### Technical Highlights:
* **Custom Architecture:** Built using custom Keras layers (Encoder, Decoder, Multi-Head Attention, Positional Encoding).
* **Optimized Parameter Count:** The model was successfully optimized to run efficiently with under 2 million parameters.
* **Flawless Accuracy:** Achieved **100% accuracy** even on deep recursion expressions (Syntactic Depth 4).

## 📈 Training Strategies: Standard vs. Progressive Learning
A key focus of this project was comparing two different training paradigms:

1. **Standard Training:** Training the model directly on the full dataset containing mixed complexities up to Depth 4.
2. **Progressive Learning (Curriculum Learning):** Training the model iteratively, starting with simple expressions (Depth 2), then fine-tuning on Depth 3, and finally on Depth 4.

### Key Findings:
While both methods achieved 100% accuracy, the **Progressive Learning** approach forces the model to solve fundamental problems before attempting complex ones. This theoretically creates a more structured internal latent space, reducing the chance of the model learning "shortcuts" and making it vastly superior for **Out-of-Distribution (OOD)** generalization.

## 🚀 How to Run
The entire project is contained within a well-documented Jupyter Notebook.

1. Clone the repository:
   ```bash
   git clone [https://github.com/YourUsername/transformer-infix-postfix.git](https://github.com/YourUsername/transformer-infix-postfix.git)
