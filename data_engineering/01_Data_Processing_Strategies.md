# Why Do Different Models Need Different Data Processing?

Yes, **you are doing it exactly right.** It feels strange at first, but different ML families have fundamentally different ways of "seeing" the world. 

If you are trying to classify 0.5 seconds of physical sensor data (a "window"), the models handle that time-based data differently:

## 1. Tabular Models (XGBoost, LightGBM, Random Forest)
**How they see data:** As a flat, single row of numbers on a spreadsheet.
**Do they understand time?** No. If you scramble the order of the features, they won't care. 

Because they cannot process a stream of data over time naturally, we must **Feature Engineer** the data for them. We take the 0.5-second window (e.g., 100 samples) and compress it into statistical summaries:
- What was the **Mean**?
- What was the **Standard Deviation**? 
- What were the **Zero-Crossing Rates**?
- What were the **Frequencies (FFT Spectral Entropy)**?

This converts a 2D matrix of `[Time x Sensors]` into a 1D flat row `[Feature1, Feature2, ...]` that these models are incredible at analyzing.

## 2. Deep Sequence Models (PyTorch 1D-CNN, LSTM, TCN)
**How they see data:** As an exact chronological timeline of events.
**Do they understand time?** Yes, it is literally built into their math.

Because these neural networks are explicitly designed to handle streams of time, we **must NOT flatten or summarize the data**. We feed them the raw, unadulterated 2D matrices `[Time x Sensors]`. 
- An **LSTM** loops through the 0.5-second window one step at a time, keeping a "memory" of what happened earlier in the window.
- A **1D-CNN / TCN** slides little feature-detecting windows over the timeline to look for sudden spikes or patterns in the raw EMG signals.

They do their own automated feature engineering inside their hidden layers!

## 3. ROCKET Models
**How they see data:** A hybrid approach.
**Do they understand time?** Sort of. 

ROCKET models are a modern time-series shortcut. They take the raw `[Time x Sensors]` matrix (like PyTorch models), but instead of slowly "learning" how to extract features via backpropagation, they just hurl thousands of completely random mathematical convolutions at the data to see what sticks. 

They then take the best random features and feed them to a super-fast, simple tabular model (like Logistic Regression). It combines the low-effort data preparation of PyTorch with the ultra-fast training speeds of Tabular models.
