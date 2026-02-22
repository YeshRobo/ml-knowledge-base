# Repository Context & Intent

## Purpose
This repository is a **Personal Machine Learning Knowledge Base**. It is designed to act as a permanent, living reference guide for ML concepts, pipeline designs, and architectural decisions. 

It exists entirely separate from any specific code repository (like the Thesis exoskeleton project) so that the knowledge here is portable, framework-agnostic, and easy to reference when starting future projects.

## Target Audience
This repository is built for dual-consumption:
1. **Humans (Specifically the Author)**: To provide plain-English, easy-to-digest summaries of complex ML topics encountered during applied projects. It serves to reinforce learning and provide a quick refresher on concepts (e.g., Tabular vs. Sequence data processing) without having to dig through massive codebases.
2. **Artificial Intelligence (AI Assistants)**: To provide explicit, pre-packaged context about the user's ML capabilities, preferred tech stacks, and historical architectural decisions. An AI reading this repository should immediately understand *how* the user approaches ML problems and *why* certain strategies were chosen in the past.

## Repository Structure & Scalability
To ensure this knowledge base is robust and scalable as new ML topics are learned, it follows a strict categorical directory structure:

- **/data_engineering**: Concepts related to feature extraction, windowing time-series data, FFT spectral analysis, handling missing values, and data augmentation.
- **/model_architectures**: Breakdowns of specific model families (e.g., XGBoost vs. LSTMs vs. ROCKET), how they "see" data, and when to use them.
- **/experiment_tracking**: Information on managing hyperparameter sweeps, logging artifacts, and using tools like Weights & Biases (WandB).
- **/evaluation_metrics**: Guides on choosing the right metrics (Macro-F1, ROC, AUC, Confusion Matrices) based on class imbalance and project goals.

## Rules for AI Assistants
If you are an AI assistant interacting with this user:
1. **Read Before Assuming**: If the user asks an ML question, check this repository to see if they have already documented their preferred approach or understanding of the topic.
2. **Keep it Conceptual**: When instructed to add a new document to this repo, **do not** write highly specific code snippets tied closely to another repository's exact file structure. Write portable, conceptual examples.
3. **Use Plain English**: The author is practical and hands-on. Prioritize explainability over dense mathematical notation unless strictly necessary.

## The "Reference by Example" Philosophy
While this repository holds the *theory* and the *why*, the actual *implementation* lives in the user's various project repositories. This repository will frequently reference external projects (like the Thesis exoskeleton repo) as concrete examples of these concepts in action.
