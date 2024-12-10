# IMPROVING SSVEP SPELLERS WITH DATA AUGUMENTATION AND LANGUAGE MODELS

## INTRODUCTION

In this project, we focused on leveraging language models to complement SSVEP spellers by predicting the next word, enhancing contextual accuracy, and improving the overall communication experience in brain-computer interface systems.

SSVEP spellers are brain-computer interface (BCI) systems that enable users to type by focusing on flickering stimuli on a screen, with each stimulus associated with a unique frequency detected through EEG signals. These systems translate brain responses into commands or text, providing a communication tool for individuals with severe motor impairments.

In SSVEP spellers, each letter (stimulus) is associated with a unique frequency. Users are exposed to these flickering stimuli, and their brain generates corresponding electrical responses. These signals are recorded through EEG, and the data is then used to train an EEGNet model to decode the brain's responses and predict the focused letter, enabling text input through the BCI system.

## DATA

The data used in this project comes from a benchmark SSVEP dataset acquired with a 40-target BCI speller, as described by Yijun Wang et al. in their paper [A Benchmark Dataset for SSVEP-Based Brain-Computer Interfaces](https://pubmed.ncbi.nlm.nih.gov/27849543/). The dataset includes 64-channel EEG data from 35 healthy subjects (8 experienced and 27 naïve), recorded during a cue-guided target selection task. The virtual keyboard of the speller consisted of 40 visual flickers, with frequencies ranging from 8 Hz to 15.8 Hz, coded using a joint frequency and phase modulation (JFPM) approach. Each trial lasted five seconds, and the data includes six blocks of 40 trials per subject, with the stimuli presented in a random order. This high-quality dataset is valuable for benchmarking stimulus coding, target identification methods, and BCI performance evaluation, and is freely available for further research and computational modeling.

## DATA AUGUMENTATION TECHNIQUES WE EMPLOYED

In this project, we explored several data augmentation techniques to improve the performance and generalization of the EEGNet model for SSVEP spellers. The main goal of data augmentation was to enhance the robustness of the model, particularly in real-world scenarios where EEG signals may be noisy or variable. The techniques we tried included:

1. **Random Impulse Noise**: Impulse noise is injected in the frequency domain by randomly modifying the frequency components with random magnitudes. This simulates sudden bursts of noise in the signal.
2. **Phase Noise**: Gaussian noise is applied to the phase of the EEG signal in the frequency domain. This helps the model handle phase-related variabilities in the signals.
3. **Magnitude Noise**: Gaussian noise is added to the magnitude of the frequency components, allowing the model to deal with fluctuations in signal strength across different frequencies.
4. **Spatial (Time-domain) Noise**: Gaussian noise is directly added to the time-domain EEG signal, mimicking real-world environmental noise or artifacts that might occur in EEG recording.
5. **Frequency Masking**: Random sections of the frequency spectrum are masked out, forcing the model to focus on the remaining relevant frequencies and simulating missing or corrupted frequency data.
6. **Time Masking**: Random time segments in the EEG signal are masked, which simulates missing or corrupted time-domain data, ensuring the model can handle incomplete signals.

 time masking was the most effective augmentation technique for improving the model’s performance in the context of SSVEP spellers, while the other techniques had limited impact.

