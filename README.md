# Domain-Adapting Qwen2.5-1.5B-Instruct for Coding Question Answering Using QLoRA

## Project Overview

This project demonstrates parameter-efficient fine-tuning of a small open-weight Large Language Model (LLM) using Quantized Low-Rank Adaptation (QLoRA).

The objective is to adapt the general-purpose **Qwen2.5-1.5B-Instruct** model to the **coding and programming domain** using the **CodeAlpaca-20k** dataset while training only a small fraction of the model parameters.

Instead of updating all 1.55 billion parameters, LoRA trains only lightweight adapter layers, significantly reducing computational cost and memory requirements.

---

## Problem Statement

General-purpose instruction-tuned models can answer programming questions reasonably well but are not optimized for a specific coding style or domain.

The goal of this project is to:

* Adapt a small open-weight model to coding-related tasks.
* Train only a small subset of parameters using LoRA.
* Evaluate whether domain adaptation improves coding-focused responses.
* Demonstrate efficient fine-tuning on limited hardware.

---

## Model

**Base Model**

* Qwen2.5-1.5B-Instruct

**Fine-Tuning Method**

* QLoRA
* 4-bit Quantization (NF4)
* LoRA Rank (r): 16
* LoRA Alpha: 32
* LoRA Dropout: 0.05

---

## Dataset

**Dataset Used**

* CodeAlpaca-20k

The dataset contains instruction-response pairs focused on:

* Python Programming
* Algorithms
* Data Structures
* SQL
* Debugging
* Software Engineering Concepts

Example:

### Instruction

Explain the concept of Convolutional Neural Networks.

### Response

Convolutional Neural Networks (CNNs) are a type of deep learning neural network used primarily in image processing and computer vision tasks.

---

## Data Preparation

The dataset was converted into the following format:

```text
### Instruction:
<instruction>

### Response:
<output>
```

The data was shuffled and split into:

* Training Set: 4,500 samples
* Validation Set: 500 samples

---

## Training Configuration

| Parameter             | Value     |
| --------------------- | --------- |
| Epochs                | 2         |
| Learning Rate         | 2e-4      |
| Batch Size            | 2         |
| Gradient Accumulation | 4         |
| Quantization          | 4-bit NF4 |
| LoRA Rank             | 16        |

---

## Parameter Efficiency

| Metric               | Value         |
| -------------------- | ------------- |
| Total Parameters     | 1,548,072,448 |
| Trainable Parameters | 4,358,144     |
| Trainable Percentage | 0.2815%       |

Only 0.28% of model parameters were updated during training.

---

## Results

### Training Metrics

| Epoch | Training Loss | Validation Loss |
| ----- | ------------- | --------------- |
| 1     | 0.126955      | 0.125333        |
| 2     | 0.118596      | 0.124809        |

### Final Metrics

| Metric                | Value               |
| --------------------- | ------------------- |
| Final Training Loss   | 0.1186              |
| Final Validation Loss | 0.1248              |
| Training Time         | ~4 Hours 20 Minutes |

The close alignment between training and validation loss indicates good generalization with no significant signs of overfitting.

---

## Evaluation

The base model and fine-tuned model were evaluated on unseen coding prompts including:

* Binary Search
* Breadth First Search
* Linked List Cycle Detection
* SQL Query Generation
* Array Manipulation

### Observations

* Fine-tuned model produced more concise code-focused answers.
* Performance improvements were observed on implementation-oriented tasks.
* Base model remained strong for conceptual explanations.
* Domain adaptation improved specialization while preserving overall coding ability.

---

## Key Learnings

Through this project I learned:

* Parameter-Efficient Fine-Tuning (PEFT)
* LoRA Architecture
* QLoRA and 4-bit Quantization
* Instruction Tuning
* Dataset Preparation for LLMs
* Evaluation of Fine-Tuned Language Models
* Efficient Training on Limited Hardware

---

## Technologies Used

* Python
* PyTorch
* Hugging Face Transformers
* PEFT
* BitsAndBytes
* Datasets
* Kaggle GPU Environment

---

## Conclusion

This project successfully demonstrated domain adaptation of Qwen2.5-1.5B-Instruct using QLoRA.

By training only 4.36 million parameters (0.28% of the model), the system was adapted to coding-related question answering while maintaining strong validation performance and low computational requirements.

The results show that QLoRA is an effective strategy for specializing large language models for domain-specific tasks without requiring full model fine-tuning.
