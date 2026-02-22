# Comparing Model Performance Characteristics

When choosing a model for a robotics or embedded project, accuracy is only half the battle. You also have to consider **Computation Cost** (how hard it is on your CPU/GPU) and **Inference Time** (how long it takes to make a prediction).

Here is how our three model families compare:

## 1. ROCKET Models
**Best for**: Fast prototyping and CPU-constrained devices.

- **Training Time**: ⚡⚡⚡ Blazing Fast (Seconds)
- **Inference Speed**: ⚡⚡⚡ Near Instantaneous (< 1ms per window)
- **Computation Cost (CPU/GPU)**: Very Low. ROCKET only uses standard matrix math and random convolutions.
- **Why use it?**: If you need to run a model on a low-powered Raspberry Pi or microcontroller and don't want to wait hours to train a neural network, ROCKET is usually the best choice.

## 2. Tabular Models (XGBoost, LightGBM, Random Forest)
**Best for**: Getting the absolute highest accuracy when you have cleanly extracted features.

- **Training Time**: ⚡⚡ Fast (Minutes)
- **Inference Speed**: ⚡⚡ Very Fast (~1-5ms per window)
- **Computation Cost (CPU/GPU)**: Low. Decision trees are highly optimized and only require simple `if/else` checks.
- **The Catch**: While the *model* is extremely fast, you must manually compute the features (Mean, STD, FFT, etc.) before feeding data to it. Calculating those features at runtime can add a tiny bit of delay.

## 3. Deep Sequence Models (PyTorch 1D-CNN, TCN, LSTM)
**Best for**: Complex, non-linear signals where hand-crafted features (like Mean/STD) aren't capturing the patterns.

- **Training Time**: 🐢 Slow (Hours to Days, often requires a GPU)
- **Inference Speed**: ⚡ Moderate (~5-20ms per window)
- **Computation Cost (CPU/GPU)**: High. Neural networks involve massive matrix multiplications.
- **Why use it?**: LSTMs and TCNs are incredibly powerful if you have massive amounts of data and strict chronological dependencies. However, they are often overkill for simple physical classification tasks and can bottleneck the control loops of real-time robots.

## Summary Matrix

| Model Family | Training Speed | Prediction Speed | Hardware Cost | Flexibility |
|---|---|---|---|---|
| **ROCKET** | Seconds | < 1ms | Low | High |
| **Tabular Trees** | Minutes | 1-5ms* | Low | Low (Requires feature extraction) |
| **PyTorch NNs** | Hours | 5-20ms | High (GPU preferred) | Very High |

*\*Note: Tree inference is fast, but you must factor in the time taken to run the FFTs/feature extraction on your robot.*
