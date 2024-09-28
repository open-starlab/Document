Event_Model Class
=========================
This class provides a framework for modeling soccer events, including training and inference capabilities using various model architectures.

Initialization
--------------
.. method:: __init__(model_name, config=None)

   Initializes the event model with the specified model name and configuration.

   :param model_name: (str) Name of the model to be used. Supported models include:
   
       - 'FMS'
       - 'LEM_action'
       - 'LEM'
       - 'MAJ'
       - 'NMSTPP'
       - 'Seq2Event'
   :param config: (str, optional) Path to a YAML configuration file. If not provided, the default settings will be loaded.
   :raises FileNotFoundError: If the specified configuration file does not exist.
   :raises ValueError: If the model name is 'MAJ', Optuna will be disabled.

Methods
-------
.. method:: train()

   Trains the specified model based on the configuration. The method selects the appropriate training routine depending on the model name and whether Optuna is enabled.

   :raises ValueError: If the model name is unknown.

.. method:: inference(model_path, model_config, train_path=None, valid_path=None, save_path=None, simulation=False, random_selection=True, max_iter=20, min_max_dict_path=None)

   Conducts inference using the trained model. It saves the results to specified paths and can perform simulations if indicated.

   :param model_path: (str) Path to the saved model.
   :param model_config: (str) Path to the JSON configuration file for the model.
   :param train_path: (str, optional) Path to the training dataset. Defaults to the path defined in the model configuration if not provided.
   :param valid_path: (str, optional) Path to the validation dataset. Defaults to the path defined in the model configuration if not provided.
   :param save_path: (str, optional) Directory to save inference results. Defaults to the path defined in the model configuration.
   :param simulation: (bool, optional) Flag indicating whether to perform a simulation. Defaults to False.
   :param random_selection: (bool, optional) Flag for random selection in simulation. Defaults to True.
   :param max_iter: (int, optional) Maximum number of iterations for simulation. Defaults to 20.
   :param min_max_dict_path: (str, optional) Path to the min-max normalization dictionary.
   :raises ValueError: If neither `train_path` nor `min_max_dict_path` are provided, or if the model name is unknown.
   :return: Depending on the simulation flag, returns either the inferenced data or simulation results along with evaluation metrics.
