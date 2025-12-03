Event_Modeling Package
==================================

The structure of the Event_Modeling package is as follows:

structure
---------
.. code-block:: text
    
    └── main_class.py  #main class for the event data
    └── Sports
        └── soccer
            └── application  #main class for the event data
            └── dataloaders #the dataloaders for model training and simulation
            └── inference # the inference and simulation functions
            └── main_class_soccer #main class for the soccer event data
            └── models
                └── model_yaml #the config files for models
                └── models.py #the models for the soccer event
            └── trainers # the train and epoch functions
            └── utils #cost functions and the preprocessing functions
