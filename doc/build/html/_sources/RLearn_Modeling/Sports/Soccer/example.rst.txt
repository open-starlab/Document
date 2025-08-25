Example: Train and Visualize RLearn Model
=============================================
To train and visualize the RLearn model, you can utilize the following code snippets.

Run All at Once
-----------------------------

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


Spliting Test and Train Data
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


Train the RLearn Model
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


Visualize the Q-values
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
