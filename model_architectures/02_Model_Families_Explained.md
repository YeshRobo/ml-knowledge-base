# Model Families Explained

Here is a quick cheat-sheet for the three types of models we are comparing in your pipeline.

## 1. Tabular Models (The Classics)
These are models that use Decision Trees under the hood. They play a game of "20 Questions" with your data (e.g., "Is the EMG average > 5.2? If yes, is the pitch velocity < 0.1?"). 
- **Random Forest**: Builds hundreds of independent, random decision trees and averages their votes. Very resilient, hard to ruin, but slightly slower to predict.
- **XGBoost / LightGBM**: These are "Gradient Boosted" trees. Instead of building independent trees, they build trees sequentially—each new tree specifically tries to fix the mistakes of the previous tree. 
    - *Pros*: Usually the absolute highest accuracy on tabular data.
    - *Cons*: Highly prone to overfitting if you don't tune them properly.

## 2. Sequence Neural Networks (PyTorch)
These are Deep Learning models specifically designed to read signals over time.
- **1D-CNN (Convolutional Neural Network)**: Sweeps a filter across the time axis (like looking through a sliding slit) to find shapes in the waveform. Very fast to run on a GPU.
- **TCN (Temporal Convolutional Network)**: A more advanced CNN that looks at wider and wider gaps of time as it goes deeper, allowing it to understand long-term context without forgetting the details.
- **LSTM (Long Short-Term Memory)**: A recurrent network that processes the data step-by-step and maintains a "hidden memory state." 
    - *Pros*: Excellent for human speech or very long dependencies.
    - *Cons*: Usually much slower to train than CNNs, and frequently over-kill for 0.5 second windows of physical sensor data.

## 3. ROCKET (Random Convolutional Kernel Transform)
This is currently considered by many researchers to be the State-of-the-Art baseline for time-series classification.
- It doesn't "learn" feature extractors. It just uses thousands of random, fixed extractors, then trains a simple Logistic Regression classifier to figure out which of those random features ended up being useful.
- *Pros*: Mind-blowingly fast to train (often takes 1 second vs. 5 hours for an LSTM), and usually matches or beats deep neural networks in accuracy.
