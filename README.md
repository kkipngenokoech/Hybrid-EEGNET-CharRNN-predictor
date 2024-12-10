# IMPROVING SSVEP SPELLERS WITH DATA AUGUMENTATION AND LANGUAGE MODELS

## INTRODUCTION

In this project, we focused on leveraging language models to complement SSVEP spellers by predicting the next word, enhancing contextual accuracy, and improving the overall communication experience in brain-computer interface systems.

SSVEP spellers are brain-computer interface (BCI) systems that enable users to type by focusing on flickering stimuli on a screen, with each stimulus associated with a unique frequency detected through EEG signals. These systems translate brain responses into commands or text, providing a communication tool for individuals with severe motor impairments.

In SSVEP spellers, each letter (stimulus) is associated with a unique frequency. Users are exposed to these flickering stimuli, and their brain generates corresponding electrical responses. These signals are recorded through EEG, and the data is then used to train an EEGNet model to decode the brain's responses and predict the focused letter, enabling text input through the BCI system.
