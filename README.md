# IMPROVING SSVEP SPELLERS WITH DATA AUGUMENTATION AND LANGUAGE MODELS

## INTRODUCTION

In this project, we focused on leveraging language models to complement SSVEP spellers by predicting the next word, enhancing contextual accuracy, and improving the overall communication experience in brain-computer interface systems.

SSVEP spellers are brain-computer interface (BCI) systems that enable users to type by focusing on flickering stimuli on a screen, with each stimulus associated with a unique frequency detected through EEG signals. These systems translate brain responses into commands or text, providing a communication tool for individuals with severe motor impairments.

In SSVEP spellers, each letter (stimulus) is associated with a unique frequency. Users are exposed to these flickering stimuli, and their brain generates corresponding electrical responses. These signals are recorded through EEG, and the data is then used to train an EEGNet model to decode the brain's responses and predict the focused letter, enabling text input through the BCI system.

## ARCHITECTURE

We used EEGNet as our baseline model for classifying EEG signals in our SSVEP speller task, benefiting from its efficient feature extraction with depthwise and separable convolutions. Credit goes to the authors of **"EEGNet: a compact convolutional neural network for EEG-based brain–computer interfaces"** (Lawhern et al., 2018, *Journal of Neural Engineering*, DOI: [10.1088/1741-2552/aace8c](https://doi.org/10.1088/1741-2552/aace8c)). Their models can be found on GitHub at this [link](https://github.com/vlawhern/arl-eegmodels)

## DATA

The data used in this project comes from a benchmark SSVEP dataset acquired with a 40-target BCI speller, as described by Yijun Wang et al. in their paper [A Benchmark Dataset for SSVEP-Based Brain-Computer Interfaces](https://pubmed.ncbi.nlm.nih.gov/27849543/). The dataset includes 64-channel EEG data from 35 healthy subjects (8 experienced and 27 naïve), recorded during a cue-guided target selection task. The virtual keyboard of the speller consisted of 40 visual flickers, with frequencies ranging from 8 Hz to 15.8 Hz, coded using a joint frequency and phase modulation (JFPM) approach. Each trial lasted five seconds, and the data includes six blocks of 40 trials per subject, with the stimuli presented in a random order. This high-quality dataset is valuable for benchmarking stimulus coding, target identification methods, and BCI performance evaluation, and is freely available [here](http://bci.med.tsinghua.edu.cn/download.html) for further research and computational modeling. 

## DATA AUGUMENTATION TECHNIQUES WE EMPLOYED

In this project, we explored several data augmentation techniques to improve the performance and generalization of the EEGNet model for SSVEP spellers. The main goal of data augmentation was to enhance the robustness of the model, particularly in real-world scenarios where EEG signals may be noisy or variable. The techniques we tried included:

1. **Random Impulse Noise**: Impulse noise is injected in the frequency domain by randomly modifying the frequency components with random magnitudes. This simulates sudden bursts of noise in the signal.
2. **Phase Noise**: Gaussian noise is applied to the phase of the EEG signal in the frequency domain. This helps the model handle phase-related variabilities in the signals.
3. **Magnitude Noise**: Gaussian noise is added to the magnitude of the frequency components, allowing the model to deal with fluctuations in signal strength across different frequencies.
4. **Spatial (Time-domain) Noise**: Gaussian noise is directly added to the time-domain EEG signal, mimicking real-world environmental noise or artifacts that might occur in EEG recording.
5. **Frequency Masking**: Random sections of the frequency spectrum are masked out, forcing the model to focus on the remaining relevant frequencies and simulating missing or corrupted frequency data.
6. **Time Masking**: Random time segments in the EEG signal are masked, which simulates missing or corrupted time-domain data, ensuring the model can handle incomplete signals.

 time masking was the most effective augmentation technique for improving the model’s performance in the context of SSVEP spellers, while the other techniques had limited impact.

 ## HOW TO REPRODUCE OUR WORK

1. Download the Tsinghua Benchmark dataset from [here](http://bci.med.tsinghua.edu.cn/download.html).
2. CLone this repo or copy the main files: SSVEP_Preprocessing, EEGNet_WithDataAugmentation, and EEGNET_CharRNN.
3. For data augmentations: Run SSVEP_Preprocessing on the Benchmark dataset and give those output directories to EEGNet_WithDataAugmentation. Change the config depending on choice of data augmentations. Run the notebook.
4. For the hybrid model: Change `subject_rawdata_dir` to point to the directory that the raw Benchmark data is located. Optionally choose word list for hybrid model evaluation. Run the notebook.

 ## CONCLUSION

 To conclude, we found that time masking is a promising augmentation for EEG classification tasks. We also demonstrated that our hybrid  model can decode words at high accuracy. To scale this system for more complex tasks like paragraph-level decoding, advanced language models such as GPT will be essential. By utilizing data augmentation and language models, we are paving the way for more accurate SSVEP speller systems that can help people with disabilities communicate.


