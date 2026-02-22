# Machine Learning Knowledge Base

Welcome to your ML Documentation hub! Since you are new to Machine Learning, this directory is designed to serve as an easy-to-read reference guide for the concepts, architectures, and data processing strategies used in your jumping robot and exoskeleton project.

## Contents
1. **[Repository Context & Intent](CONTEXT.md)**: Start here. Understands how this repo is meant to be used by humans and AIs.
2. **[Data Processing Strategies](data_engineering/01_Data_Processing_Strategies.md)**: Why different model families require completely different data inputs.
3. **[Model Families Explained](model_architectures/02_Model_Families_Explained.md)**: A breakdown of the models we are using: Tabular, ROCKET, and PyTorch Deep Sequence.

*Note: This folder is initialized as its own separate Git repository! You can push it to a new GitHub repo to keep it separate from your main code, or just keep it here for easy reference.*

## How to embedding this in other projects
To include this knowledge base in any future projects, navigate to your new project's folder in the terminal and run:

```bash
git submodule add https://github.com/YeshRobo/ml-knowledge-base.git docs/ml_knowledge_base
```
