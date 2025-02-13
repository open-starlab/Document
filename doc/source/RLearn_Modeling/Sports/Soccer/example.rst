Example: Train and Visualize sarsa_attacker Model
=============================================
To train and visualize the sarsa_attacker model, you can utilize the following code snippets.

Spliting Test and Train Data
-----------------------------

.. code-block:: python

    from .soccer.main_class_soccer.main import rlearn_model_soccer
    import os

    # Set path and experiment name for split data
    input_path = '/path/to/dataprovider'
    output_path = '/path/to/dataprovider/split'

    RLearn_Model(
        input_path=input_path,
        output_path=output_path
    ).split_train_test()

Preprocess Observations
------------------------

.. code-block:: python

    from .soccer.main_class_soccer.main import rlearn_model_soccer
    import os

    # Set path and experiment name for preprocess data
    config = '/path/to/preprocessing_dataprovider.json'
    input_path = '/path/to/dataprovider/split/mini'
    output_path = '/path/to/dataprovider_simple_obs_action_seq/split/mini'

    RLearn_Model(
        config=config,
        input_path=input_path,
        output_path=output_path
        num_process=4
    ).preprocess_observations(batch_size=64)


Train the sarsa_attacker Model
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
        config=config
    ).train_model(
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

    RLearn_Model().visualize_q_values(
        model_name=model_name,
        checkpoint_path=checkpoint_path,
        match_id='2022100106',
        sequence_id=0
    )
