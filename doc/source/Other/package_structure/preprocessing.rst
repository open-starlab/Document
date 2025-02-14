Pre_Processing Package
==================================

The structure of the Pre_Processing package is as follows:

structure
---------
.. code-block:: text

    ├── Animal
    │   └── TBA
    └── Sports
        └── event_data
            └── event_class.py  #main class for the event data
            └── soccer
                └── soccer_event_class.py  #sub class for the soccer event data
                └── soccer_event_load_data.py  #load data for the soccer event
                └── soccer_event_processing.py  #preprocess data for the soccer event
                └── soccer_plot_row.py  #plot the row data for the soccer event
            └── handball
                └── TBA
            └── rocket_league
                └── TBA
        └── SAR_data
            └── SAR_class.py  #main class for the SAR data
            └── soccer
                └── cleaning #cleaning files for the soccer SAR data
                └── state_preprocess #state preprocess files for the soccer SAR data
                └── utils #utils files for the soccer SAR data
                └── soccer_SAR_class.py  #sub class for the soccer SAR data
                └── soccer_SAR_load_data.py  #load data for the soccer SAR data
                └── soccer_SAR_processing.py  #preprocess data for the soccer SAR data
                └── soccer_SAR_cleaning.py  #cleaning data for the soccer SAR data
                └── soccer_SAR_state.py #state for the soccer SAR data
                └── constants.py #constants for the soccer SAR data
                └── dataclass.py #dataclass for the soccer SAR data
                └── env.py #source for the soccer SAR data
