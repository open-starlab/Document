Framework
====================================

This section details the framework for data preparation, model training, and inference for Play Phase estimation.

Framework Overview
------------------

Data Acquisition
~~~~~~~~~~~~~~~~
To train a model from scratch:
1. **Raw Tracking Data**: Obtain from the `SoccerTrack-v2 <https://atomscott.github.io/SoccerTrack-v2/>`_ dataset. The required files differ depending on the **Match ID**:

   * **Match ID >= 130000** (e.g., Match ID: 132831)
     * **Event Data**: ``raw/{MatchID}/{TeamA} vs {TeamB} player_nodes.csv``
     * **Tracking Data**: ``raw/{MatchID}/{MatchID}_{1,2,3}_frame_data.json``
     * **Meta Data**: ``raw/{MatchID}/{MatchID}_metadata.json``

   * **Match ID < 130000** (e.g., Match ID: 117092)
     * **Event Data**: ``raw/{MatchID}/{TeamA} vs {TeamB} player_nodes.csv``
     * **Tracking Data**: ``raw/{MatchID}/{MatchID}_tracker_box_data.xml``
     * **Meta Data**: ``raw/{MatchID}/{MatchID}_tracker_box_metadata.xml``

    **Directory Structure Example:**

    .. code-block:: text

        SoccerTrack-v2
        └── raw/
            ├── 117092/  (Match ID < 130000)
            │   ├── 筑波大学 B vs 筑波大学 - C1 player_nodes.csv
            │   ├── 117092_tracker_box_data.xml
            │   └── 117092_tracker_box_metadata.xml
            ├── ...
            └── 132831/  (Match ID >= 130000)
                ├── 中央学院大学 vs 筑波大学 - C1 player_nodes.csv
                ├── 132831_1_frame_data.json
                ├── 132831_2_frame_data.json
                ├── 132831_3_frame_data.json
                └── 132831_metadata.json

2. **Ground Truth Labels**: Download the play phase labels from the `PhaseLearnDataset <https://drive.google.com/drive/folders/1m8o531rpDfNjEszU6k2waYMhXY4upU7u?usp=sharing>`_.

    .. code-block:: text

        PhaseLearn
        └── annotation/
            ├── 117092/
            │   ├── 117092_00_01-04_18_annotation.csv
            │   ├── 117092_05_47-08_44_annotation.csv
            │   ├── 117092_09_09-10_07_annotation.csv
            │   ├── 117092_29_36-31_03_annotation.csv
            │   ├── 117092_34_59-37_13_annotation.csv
            │   ├── 117092_46_17-48_09_annotation.csv
            │   └── 117092_52_30-53_17_annotation.csv
            ├── ...
            └── 132877/
                ├── ...

Preprocessing
~~~~~~~~~~~~
Before training or inference, you must generate `**Phase Data**<https://openstarlab.readthedocs.io/en/latest/Pre_Processing/Sports/Phase_data/index.html>`_ using the ``Pre-Processing`` package. This ensures all tracking and event data are standardized into the required format.


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