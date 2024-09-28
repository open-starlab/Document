Example: Train and Inference NMSTPP model
=============================================
To train, infer, and simulate using the NMSTPP model, you can utilize the following code snippets.

Training the NMSTPP Model
---------------------------

.. code-block:: python

    from event import Event_Model
    import os

    # Initialize the NMSTPP model
    model = Event_Model('NMSTPP', 'path/to/train_NMSTPP.yaml')
    # Uncomment to use Optuna for hyperparameter optimization
    # model = Event_Model('NMSTPP', 'path/to/train_NMSTPP_optuna.yaml')
    
    # Train the model
    model.train()

Inference
----------

After training, you can perform inference. Here’s how to do it:

.. code-block:: python

    model_path = 'path/to/_model_1.pth'
    model_config = 'path/to/hyperparameters.json'

    # Simple inference
    model.inference(model_path, model_config)

    # Simulation with evaluation
    model.inference(model_path, model_config, simulation=True, random_selection=True, max_iter=20)

Inference on Other Data
------------------------

To run inference on other datasets, set the `train_path` in the YAML file to `None`. Here’s an example:

.. code-block:: python

    min_max_dict_path = 'path/to/min_max_dict.json'

    # Simple inference
    model.inference(model_path, model_config, min_max_dict_path=min_max_dict_path)

    # Simulation with evaluation
    model.inference(model_path, model_config, simulation=True, random_selection=True, max_iter=20, min_max_dict_path=min_max_dict_path)

YAML Configuration for Training the NMSTPP Model
---------------------------------------------------

The YAML file for training the NMSTPP model should look like this:

.. code-block:: yaml

    # OpenStarLab Event Modeling, Apache-2.0 license
    # UEID data (with openstarlab-preprocessing package) and NMSTPP model


    # Training parameters
    train_path: /path/to/train.csv                                                            # Path to the train set
    valid_path: /path/to/valid.csv                                                            # Path to the valid set
    save_path: /path/to/save                                                                  # Path to save the training results 
    test: True                                                                                # Test the model training 
    num_epoch: 50
    print_freq: 1
    early_stop_patience: 3
    dataloader_num_worker: 4
    device: None                                                                              #when None, device = torch.device('cuda' if torch.cuda.is_available() else 'cpu') 

    # Input features
    basic_features: ['action', 'delta_T', 'start_x','start_y'] 
    other_features: ['team','home_team','success','seconds','deltaX','deltaY','distance','dist2goal','angle2goal']
    use_other_features: True
    num_actions: 9 
    seq_len: 1

    # Model Hyperparameters (use all lists for optuna or all value for specified hyperparameters)
    optuna: False
    optuna_n_trials: 100

    learning_rate: 0.01
    eps: 1e-16
    batch_size: 256

    action_embedding_out_len: 9 #num_actions
    scale_grad_by_freq: True
    continuous_embedding_output_len: 12 #len(features)-1

    multihead_attention: 1 #fix to 1 given the previous papers
    hidden_dim: 1024
    feature_embedding_output_len: 21 #len(features)-1 + action_embedding_out_len

    NN_deltaT_num_layers: 1
    NN_location_num_layers: 1
    NN_action_num_layers: 2

YAML Configuration for Optuna Hyperparameter Optimization
-----------------------------------------------------------

When using Optuna for hyperparameter optimization, your YAML file should resemble the following:


.. code-block:: yaml

    # OpenStarLab Event Modeling, Apache-2.0 license
    # UEID data (with openstarlab-preprocessing package) and NMSTPP model


    # Training parameters
    train_path: /path/to/train.csv                                                            # Path to the train set
    valid_path: /path/to/valid.csv                                                            # Path to the valid set
    save_path: /path/to/save                                                                  # Path to save the training results 
    test: True                                                                                # Test the model training 

    num_epoch: 50
    print_freq: 1
    early_stop_patience: 5
    dataloader_num_worker: 4
    device: None                                                                              #when None, device = torch.device('cuda' if torch.cuda.is_available() else 'cpu') 

    # Input features
    basic_features: ['action', 'delta_T', 'start_x','start_y'] 
    other_features: ['team','home_team','success','seconds','deltaX','deltaY','distance','dist2goal','angle2goal']
    use_other_features: True
    num_actions: 9 
    seq_len: 40

    # Model Hyperparameters (use all lists for optuna or all value for specified hyperparameters)
    optuna: True
    optuna_n_trials: 100

    learning_rate: [0.01]
    eps: [1e-16]
    batch_size: [256]

    action_embedding_out_len: [9] #num_actions
    scale_grad_by_freq: [True]
    continuous_embedding_output_len: [12] #len(features)-1

    multihead_attention: [1] #fix to 1 given the previous papers
    hidden_dim: [16,256,512,1024,2048]
    feature_embedding_output_len: [21] #len(features)-1 + action_embedding_out_len

    NN_deltaT_num_layers: [1,2,3]
    NN_location_num_layers: [1,2,3]
    NN_action_num_layers: [1,2,3]
