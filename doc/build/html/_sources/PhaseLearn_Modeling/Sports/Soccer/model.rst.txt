Models and Framework
====================================

This section details the framework for data preparation, model training, and inference for Play Phase estimation.

Framework Overview
------------------

Preprocessing
~~~~~~~~~~~~
Before training or inference, you must generate **Phase Data** using the ``Pre-Processing`` package. This ensures all tracking and event data are standardized into the required format.

Data Acquisition
~~~~~~~~~~~~~~~~
To train a model from scratch:
1. **Raw Tracking Data**: Obtain from the `SoccerTrack-v2 <https://github.com/Hiro-Nishio/SoccerTrackV2>`_ dataset.
2. **Ground Truth Labels**: Download the play phase labels from the `provided link <INSERT_GT_LINK_HERE>`_.

Training Pipeline
~~~~~~~~~~~~~~~~
The framework uses the ``load_train_data()`` and ``preprocessing_data()`` functions to convert raw data into sequences and labels. Training is executed via the ``train()`` method of the ``phase_model_soccer`` class.

Inference and Analysis
~~~~~~~~~~~~~~~~~~~~~~
The ``phase_model_soccer`` class provides three specialized functions for inference:

- **quantitative_test()**: Evaluates the model using the test split of the dataset created during preprocessing. This is used for standard performance benchmarking (e.g., accuracy, F1-score).
- **qualitative_analysis()**: Uses sample sequences from datasets with ground truth (like SoccerTrack-v2) to analyze time-series prediction transitions and model behavior.
- **live_prediction()**: Conducts inference on any tracking data, even those without ground truth labels, for real-world application.

Model Architectures
-------------------
The framework supports four state-of-the-art spatio-temporal architectures:

1. **Transformer**: A standard spatio-temporal transformer leveraging self-attention mechanisms.
2. **Baller2vec**: An architecture designed to capture agent-based dynamics in sports.
3. **GCN + Transformer**: Integrates Graph Convolutional Networks to model spatial relationships between players before temporal processing.
4. **GAT + Transformer**: Utilizes Graph Attention Networks to dynamically weight player interactions within the spatio-temporal sequence.