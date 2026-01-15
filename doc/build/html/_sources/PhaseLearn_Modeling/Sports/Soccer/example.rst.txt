Example: Training and Inference
================================

To utilize the Play Phase estimation framework, you can follow these code snippets using the ``Phase_Model`` class.

1. Training
--------

.. code-block:: python

    from phase_model import Phase_Model

    # Initialize model (e.g., 'gcn_transformer')
    model = Phase_Model(model_name='gcn_transformer', team_mode='1team_mode')
    
    # Run training with YAML config
    train_config = 'phase/sports/soccer/models/model_yaml/train_gcn_transformer.yaml'
    model.train(train_config)

YAML Configuration Example

.. code-block:: yaml

    # -----------------------------------
    # DATA
    # -----------------------------------
    data:
        train_sequence_np_path: 'data/train_data/bepro/sequence_np.npy'
        train_label_np_path: 'data/train_data/bepro/label_np.npy'
        save_dir: '.'
        mode: '2team_mode'
        augmentation: True

    # -----------------------------------
    # MODEL PARAMETERS (Baller2Vec)
    # -----------------------------------
    model:
        name: 'transformer'
        # --- Embedding and Input ---
        num_players: 22            # Number of players per sequence (on the pitch)
        hidden_dim: 64           # Embedding dimension
        # seq_len: 100             # Input sequence length
        # embed_before_mlp: True   # Use MLP after embedding (boolean flag)
        # --- Transformer/MLP ---
        num_heads: 4               # Number of transformer heads
        num_layers: 2              # Number of transformer layers
        # dim_feedforward: 256     # Dimension of FFN layer
        # mlp_layers: [60, 64]     # Node count for the final MLP layers
        # dropout: 0.0             # Dropout rate
        # --- Output ---
        target_size:
            1team_mode: 9          # Standard number of output classes (e.g., 9 classes)
            2team_mode: 18         # Output classes for 2-team augmentation mode

    # -----------------------------------
    # TRAINING PARAMETERS
    # -----------------------------------
    training:
        batch_size: 128
        num_epochs: 1
        lr: 0.00001
        patience: 10
        optimizer: 'AdamW'        # Optimization method
        loss_function: 'HuberLoss' # Loss function
        device: 'cuda:0'

2. Inference
------------------------

2.1. Quantitative Evaluation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: python

    # Run evaluation on test dataset
    model_config = 'model/gat_transformer/1team_mode/20260110_191939/run_1/hyperparameters.json'
    model.quantitative_test(model_config)

2.2. Qualitative Analysis
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: python

    # Analyze specific sequences with ground truth
    analysis_data = {
        'sequence_np_path': 'data/inference/117093_sequence_np.npy',
        'label_np_path': 'data/inference/117093_label_np.npy',
        'time_np_path': 'data/inference/117093_time_np.npy',
        'phase_data_path': 'data/phase_data/117093_main_data.csv',
        'phase_annotation_data_path': 'data/phase_annotation/117093_annotation.csv'
    }
    model.qualitative_analysis(model_config, **analysis_data)

2.3. Live Prediction
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: python

    # Inference on unlabeled tracking data
    prediction_data = {
        'sequence_np_path': 'data/inference/117092_sequence_np.npy',
        'time_np_path': 'data/inference/117092_time_np.npy',
        'phase_data_path': 'data/phase_data/117092_main_data.csv'
    }
    model.live_prediction(model_config, **prediction_data)