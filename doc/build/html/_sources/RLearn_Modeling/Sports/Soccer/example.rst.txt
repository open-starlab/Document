Example: Train and Visualize RLearn Model
=============================================
To train and visualize the RLearn model, you can utilize the following code snippets.

Automated Pipeline Execution (Recommended)
--------------------------------------------
The RLearn model now supports fully automated pipeline execution through the ``run_rlearn`` method. This approach allows you to execute the entire machine learning workflow in a single command, including data splitting, preprocessing, training, and visualization. The pipeline automatically manages file paths, configuration updates, and error handling.

**Benefits of automated execution:**

- **Simplified workflow**: Execute all steps with one command
- **Automatic path management**: Input/output paths are managed automatically
- **Error handling**: Built-in error detection and recovery
- **Configuration management**: Settings are automatically updated between steps
- **Reduced manual intervention**: Minimizes the risk of configuration errors

.. code-block:: python

    from .soccer.main_class_soccer.main import rlearn_model_soccer
    import os

    # Set path and experiment name for split data
    config = '/path/to/exp_config.json'
    input_path = '/path/to/dataprovider'
    output_path = '/path/to/dataprovider_simple_obs_action_seq/split/'
    exp_name = 'sarsa_attacker'
    run_name = 'test'
    accelerator = 'gpu'
    devices = 1
    strategy = 'auto'

    RLearn_Model(
        state_def="PVS",
        config=config,
        input_path=input_path,
        output_path=output_path,
    ).run_rlearn(
        run_split_train_test=True,
        run_preprocess_observation=True, 
        batch_size=64,
        run_train_and_test=True, 
        exp_name=exp_name, 
        run_name=run_name, 
        accelerator=accelerator, 
        devices=devices, 
        strategy=strategy,
        run_visualize_data=True,
        model_name='exp_config',
        checkpoint_path='/path/to/output/sarsa_attacker/test/checkpoints/epoch=1-step=2.ckpt',
        match_id='2022100106',
        sequence_id=0
    )

**Parameters explanation:**

- ``run_split_train_test=True``: Automatically splits data into training and testing sets
- ``run_preprocess_observation=True``: Applies preprocessing to observation data
- ``run_train_and_test=True``: Trains the model and runs evaluation
- ``run_visualize_data=True``: Generates visualization of Q-values and model outputs

The pipeline automatically manages intermediate file paths and updates configuration files as needed.

Advanced Usage: Manual Step Execution
======================================
For advanced users who need fine-grained control over each step, you can execute individual components manually. This approach is useful for debugging, custom modifications, or when you need to inspect intermediate results.

Data Splitting
-----------------------------

.. code-block:: python

    from .soccer.main_class_soccer.main import rlearn_model_soccer
    import os

    # Set path and experiment name for split data
    input_path = '/path/to/dataprovider'

    RLearn_Model(
        state_def="PVS",
        input_path=input_path
    ).run_rlearn(run_split_train_test=True)


Preprocess Observations
------------------------

.. code-block:: python

    from .soccer.main_class_soccer.main import rlearn_model_soccer
    import os

    # Set path and experiment name for preprocess data
    config = '/path/to/preprocessing_dataprovider.json'
    input_path = '/path/to/dataprovider/'
    output_path = '/path/to/dataprovider_simple_obs_action_seq/split/'

    RLearn_Model(
        state_def="PVS",
        input_path=input_path,
        output_path=output_path,
    ).run_rlearn(run_preprocess_observation=True, batch_size=64)


Model Training
-------------------------------

.. code-block:: python

    from .soccer.main_class_soccer.main import rlearn_model_soccer
    import os

    # Set path and experiment name for train model
    config = '/path/to/exp_config.json'
    exp_name = 'sarsa_attacker'
    run_name = 'test'
    accelerator = 'gpu'
    devices = 1
    strategy = 'auto'

    RLearn_Model(
        state_def="PVS",
        config=config,
    ).run_rlearn(
        run_train_and_test=True, 
        exp_name=exp_name, 
        run_name=run_name, 
        accelerator=accelerator, 
        devices=devices, 
        strategy=strategy
    )


Q-values Visualization
-----------------------

.. code-block:: python

    from .soccer.main_class_soccer.main import rlearn_model_soccer
    import os

    # Set path and experiment name for visualize data
    model_name = 'exp_config'
    checkpoint_path = '/path/to/output/sarsa_attacker/test/checkpoints/epoch=1-step=2.ckpt'

    RLearn_Model(
        state_def="PVS"
    ).run_rlearn(
        run_visualize_data=True,
        model_name=model_name,
        checkpoint_path=checkpoint_path,
        match_id='2022100106',
        sequence_id=0
    )
