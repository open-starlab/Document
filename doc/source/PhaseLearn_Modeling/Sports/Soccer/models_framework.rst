Framework
====================================

This section details the framework for data preparation, model training, and inference for Play Phase estimation.

Data Acquisition
------------------

Depending on your objective, you can either use a pre-trained model for immediate inference or collect raw data to train a model from scratch.

1. Quick Start: Using Pre-trained Models
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
If you want to perform inference immediately, obtain the pre-trained weights and configuration files.

- **Pre-trained Weights**: Download the model package from `Pre-trained Model Link <https://tsukuba.repo.nii.ac.jp/records/2021338>`_ .

    .. code-block:: text

        model/
        └── {architecture_name}/           # e.g., gat_transformer
            └── {mode_name}/               # e.g., 2team_mode
                └── {timestamp}/           # e.g., 20251221_155257
                    └── run1/
                        ├── best.pth
                        ├── hyperparameters.json
                        ├── loss.csv
                        └── model_stats.txt

2. Train a Model from Scratch
^^^^^^^^^^^^^^^^^^^^^^^^^^
To train a new model, you need both raw tracking data and specialized play phase annotations.

- **Raw Tracking Data**: Obtain from the `SoccerTrack-v2 <https://atomscott.github.io/SoccerTrack-v2/>`_ dataset. The required files depend on the **Match ID**:

    - Match ID >= 130000 (e.g., Match ID: 132831)
        - Event Data: ``raw/{MatchID}/{TeamA} vs {TeamB} player_nodes.csv``
        - Tracking Data: ``raw/{MatchID}/{MatchID}_{1,2,3}_frame_data.json``
        - Meta Data: ``raw/{MatchID}/{MatchID}_metadata.json``

    - Match ID < 130000 (e.g., Match ID: 117092)
        - Event Data: ``raw/{MatchID}/{TeamA} vs {TeamB} player_nodes.csv``
        - Tracking Data: ``raw/{MatchID}/{MatchID}_{tracker_box_data}.xml``
        - Meta Data: ``raw/{MatchID}/{MatchID}_{tracker_box_metadata}.xml``

    **Example Directory Structure (SoccerTrack-v2):**

    .. code-block:: text

        SoccerTrack-v2
        └── raw/
            ├── 117092/  (Match ID < 130000)
            │   ├── 筑波大学 B vs 筑波大学 - C1 player_nodes.csv
            │   ├── 117092_tracker_box_data.xml
            │   └── 117092_tracker_box_metadata.xml
            └── 132831/  (Match ID >= 130000)
                ├── 中央学院大学 vs 筑波大学 - C1 player_nodes.csv
                ├── 132831_1_frame_data.json
                ├── 132831_2_frame_data.json
                ├── 132831_3_frame_data.json
                └── 132831_metadata.json

- **Ground Truth Labels**: The Play Phase annotation data is not currently public. Please contact **Kento Kuroda** (`kuroda.kento@image.iit.tsukuba.ac.jp <mailto:kuroda.kento@image.iit.tsukuba.ac.jp>`_) to request access to the dataset.

    **Example Directory Structure (Annotations):**

    .. code-block:: text

        PhaseLearn
        └── annotation/
            ├── 117092/
            │   ├── 117092_00_01-04_18_annotation.csv
            │   └── ...
            └── 132877/
                └── ...

Preprocessing
------------------
Before training or inference, you must generate `**Phase Data**<https://openstarlab.readthedocs.io/en/latest/Pre_Processing/Sports/Phase_data/index.html>`_ using the ``Pre-Processing`` package. This ensures all tracking and event data are standardized into the required format.

Training Pipeline
------------------
The framework uses the ``load_train_data()`` and ``preprocessing_data()`` functions to convert raw data into sequences and labels. 
The ``augmentation()`` function then enhances the dataset by flipping spatial coordinates and swapping team positions to improve model robustness.
Training is executed via the ``train()`` method of the ``phase_model_soccer`` class.

Inference and Analysis
------------------
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