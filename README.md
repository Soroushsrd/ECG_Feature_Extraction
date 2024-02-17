# ECG Feature Extraction

This Python package provides a set of tools for analyzing electrocardiogram (ECG) signals. It includes functions for signal decomposition using wavelet transform, R-peak detection, extraction of PQRS complexes, heart rate calculation, and various feature extractions. These features would then be saved inside a data frame that can be used for machine learning purposes.


## Installation

Download the ECG_Feature_Extraction.py and import functions that you might need.

- Install the necessary dependencies using pip:

```bash
pip install -r requirements.txt
```
## Dependencies
This package relies on the following libraries:

- [NeuroKit2](https://github.com/neuropsychology/NeuroKit)

NeuroKit2 is a Python library for neurophysiological signal processing. It provides functions for processing ECG signals, including R-peak detection and heart rate analysis. For more information, visit the NeuroKit2 GitHub repository.

- [PyWavelets (pywt)](https://github.com/PyWavelets/pywt/tree/master)

PyWavelets is a Python library for wavelet transform computations. It is used in this package for signal decomposition and analysis. For more information, visit the PyWavelets GitHub repository.
## Usage

```python
import numpy as np
import pandas as pd
from ecg_analysis_toolkit import *

# Sample ECG signal data (replace this with your own data)
ecg_signal = np.random.rand(1000)

# Combine 12-lead signals into a single combined signal
weights = {'lead1': 1, 'lead2': 1, 'lead3': 2, 'lead4': 2, 'lead5': 2, 'lead6': 1,
           'lead7': 1, 'lead8': 1, 'lead9': 1, 'lead10': 1, 'lead11': 1, 'lead12': 1}
combined_signal = combine_12_leads(weights, ecg_signal)

# Perform wavelet analysis
plot_wavelet_analysis(ecg_signal, wavelet='sym4', level=3)
reconstructed_signal = wavelet_analysis(ecg_signal, wavelet='sym4', level=3)

# R peak detection
R_peaks, R_peak_values = R_finder(reconstructed_signal)
R_plot(reconstructed_signal)

# Extraction of PQRS complexes
r_peaks, r_amplitudes, p_peaks, p_amplitudes, q_peaks, q_amplitudes, s_peaks, s_amplitudes = PQRS_extraction(ecg_signal)

# Heart rate calculation
heart_rate = HR_counter(ecg_signal)

# Mean PQRS amplitude calculation
mean_r, mean_p, mean_q, mean_s = mean_PQRS_amplitude(ecg_signal)

# Wave duration calculation
r_wave_duration, p_wave_duration, pr_interval = wave_duration(ecg_signal)

# RR ratio calculation
rr_ratio = RR_ratio(ecg_signal)

# Feature extraction
features_df = extraction(combined_signal)

```
## Example Notebook
For an example of how to use these functions to analyze ECG signals from the PTB_XL database, please refer to the provided Jupyter notebook in this repository. This notebook was built upon the data provided by the physio.net database. For the PTB_XL dataset, please visit the [PhysioNet website](https://physionet.org/content/ptb-xl/1.0.3/).


## Contributing

Pull requests are welcome. For major changes, please open an issue first
to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License

This project is licensed under the [Apache License 2.0](http://www.apache.org/licenses/)
