Phase Model Class
=========================

The ``phase_model_soccer`` class provides a comprehensive framework for training and evaluating soccer-specific deep learning models using spatio-temporal tracking data.

Initialization
--------------
.. py:class:: phase_model_soccer(model_name, team_mode)

      Initializes the model wrapper with a specific architecture.

      :param str model_name: Name of the architecture to be used. Supported models:
      
            - ``'transformer'``: Standard Spatio-Temporal Transformer.
            - ``'baller2vec'``: Implementation based on the Baller2Vec architecture.
            - ``'gcn_transformer'``: Graph Convolutional Network combined with a Transformer.
            - ``'gat_transformer'``: Graph Attention Network combined with a Transformer.
      
      :param str team_mode: Specifies the prediction target configuration. Options include:
      
            - ``'1team_mode'``: Predicts only for the team attacking in the positive x-axis direction of the pitch.
            - ``'2team_mode'``: Predicts for both teams.

Methods
-------

.. py:method:: train(train_config)

      Trains the selected model architecture using the provided configuration.

      :param str train_config: Path to a YAML file containing training parameters (e.g., batch size, learning rate, and data paths).
      :raises ValueError: If the ``model_name`` provided during initialization is not supported.

    **Note**: If the NumPy sequences (``.npz`` or ``.npy``) do not exist at the paths specified in the config, the method will automatically trigger the ``preprocessing_data`` routine.

.. py:method:: quantitative_test(model_config)

      Performs a standardized evaluation on a test dataset to generate numerical performance metrics.

      :param str model_config: Path to a JSON file containing the trained model's metadata and test data paths.
      :return: Saves three CSV files (``regression.csv``, ``top_k.csv``, and ``classification.csv``) to the evaluation directory.

.. py:method:: qualitative_analysis(model_config, sequence_np_path=None, label_np_path=None, time_np_path=None, phase_data_path=None, phase_annotation_data_path=None)

      Generates sequence-level predictions for in-depth analysis of specific match phases.

      :param str model_config: Path to the model's JSON configuration.
      :param str sequence_np_path: Optional path to pre-processed test sequences.
      :param str phase_data_path: Optional path to raw phase CSV data if pre-processed files are not available.
      :return: Saves a ``qualitative_analysis.csv`` containing timestamps and model outputs.

.. py:method:: live_prediction(model_config, sequence_np_path=None, time_np_path=None, phase_data_path=None)

      Executes inference on tracking data without requiring ground-truth labels, designed for real-time or recent match analysis.

      :param str model_config: Path to the model's JSON configuration.
      :param str phase_data_path: Path to the tracking data to be analyzed.
      :return: Saves a ``live_prediction.csv`` mapping predictions to match timestamps.