SAR_Model Class
=========================
This class provides the spliting test anda train data for the SAR model, attacker simple observation, train the SAR model and visualize the Q values.

Initialization
-------------------------
.. method:: __init__(config=None)

   Initializes the SAR model with the specified configuration.

   :param model_name: (str, optional) Name of the model to be used. Defaults to 'SARSA'.
   :param config: (str) Path to a JSON configuration file.
   :param seed: (int, optional) Random seed for reproducibility. Defaults to 42.
   :param num_process: (int, optional) Number of processes to use for parallelization. Defaults to 4.
   :param input_path: (str, optional) Path to the input data. Defaults to None.
   :param output_path: (str, optional) Path to save the output data. Defaults to None.
   :raises FileNotFoundError: If the specified configuration file does not exist.


Methods
-------------------------
.. method:: split_train_test()

   Splits the input data into training and testing sets.


.. method:: preprocess_observations(batch_size)

   Preprocesses the input data to generate the observations for the attacker.


.. method:: train_model(exp_name, run_name, accelerator, devices, strategy)
    
   Trains the SAR model using the preprocessed data.

   :param exp_name: (str) Name of the experiment. Defaults to 'sarsa_attacker'.
   :param run_name: (str) Name to save in tensorflow, mlflow, etc.
   :param accelerator: (str) Accelerator to use for training. Defaults to 'auto'.
   :param devices: (int) Number of devices to use for training. Defaults to 1.
   :param strategy: (str) Controls the model distribution across training, evaluation, and prediction to be used by the Trainer. Defaults to 'auto'.


.. method:: visualize_q_values(model_name, checkpoint_path, match_id, sequence_id)

   Visualizes the Q-values for the trained SAR model.

   :param model_name: (str) Name of the model used for training.
   :param checkpoint_path: (str) Path to the saved model checkpoint.
   :param match_id: (str) Match ID you want to visualize.
   :param sequence_id: (str) Sequence ID you want to visualize.