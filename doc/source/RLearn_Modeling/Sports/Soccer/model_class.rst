RLearn_Model Class
=========================
This class provides the splitting test and train data for the SAR model, attacker simple observation, train the RLearn model and visualize the Q values.

Initialization
-------------------------
.. method:: __init__(state_def, config, seed, num_process, input_path, output_path)

   Initializes the RLearn model with the specified configuration.

   :param state_def: (str) State definition to use for the model.
   :param config: (str) Path to a JSON configuration file.
   :param seed: (int, optional) Random seed for reproducibility. Defaults to 42.
   :param num_process: (int, optional) Number of processes to use for parallelization. Defaults to 4.
   :param input_path: (str, optional) Path to the input data. Defaults to None.
   :param output_path: (str, optional) Path to save the output data. Defaults to None.


Methods
-------------------------
.. method:: split_train_test()

   Splits the input data into training and testing sets.


.. method:: preprocess_observations(batch_size)

   Preprocesses the input data to generate the observations for the attacker.

   :param batch_size: (int) Batch size for processing the data.


.. method:: train_model(exp_name, run_name, accelerator, devices, strategy)
    
   Trains the RLearn model using the preprocessed data.

   :param exp_name: (str) Name of the experiment. Defaults to 'sarsa_attacker'.
   :param run_name: (str) Name to save in tensorflow, mlflow, etc.
   :param accelerator: (str) Accelerator to use for training. Defaults to 'auto'.
   :param devices: (int) Number of devices to use for training. Defaults to 1.
   :param strategy: (str) Controls the model distribution across training, evaluation, and prediction to be used by the Trainer. Defaults to 'auto'.


.. method:: visualize_q_values(model_name, checkpoint_path, match_id, sequence_id)

   Visualizes the Q-values for the trained RLearn model.

   :param model_name: (str) Name of the model used for training.
   :param checkpoint_path: (str) Path to the saved model checkpoint.
   :param match_id: (str) Match ID you want to visualize.
   :param sequence_id: (str) Sequence ID you want to visualize.


.. method:: run_rlearn(run_split_train_test, run_preprocess_observation, run_train_and_test, run_visualize_data, batch_size, exp_name, run_name, accelerator, devices, strategy)
   
   Runs the RLearn data splitting, observation processing, model training and evaluation pipeline.

   :param run_split_train_test: (bool) Whether to run the train/validation/test split.
   :param run_preprocess_observation: (bool) Whether to run the observation preprocessing.
   :param run_train_and_test: (bool) Whether to run the model training and inference.
   :param run_visualize_data: (bool) Whether to run the data visualization.
   :param batch_size: (int) Batch size for processing the data.
   :param exp_name: (str) Name of the experiment.
   :param run_name: (str) Name of the run.
   :param accelerator: (str) Accelerator to use for training.
   :param devices: (int) Number of devices to use for training.
   :param strategy: (str) Strategy to use for training.