Download and Preprocess RoboCup2D Data
=====================================================

This script loads and preprocesses RoboCup2D data into the football SAR format.

Dependencies
------------

* `openstarlab_preprocessing`

Usage
-----

.. code-block:: python

    from preprocessing import SAR_data

    robocup_dir = "/path/to/data_folder/"
    state_def = "PVS"
    match_id = "match_001"
    config_path = "/path/to/preprocess_config.json"

    # load and preprocess RoboCup2D (single file)
    Soccer_SAR_data(
        data_provider='robocup_2d',
        state_def=state_def,
        data_path=robocup_dir,
        match_id=match_id,
        config_path=config_path,
        preprocess_method='SAR'
    ).preprocess_data()

    # load and preprocess RoboCup2D (multiple files)
    Soccer_SAR_data(
        data_provider='robocup_2d',
        state_def=state_def,
        data_path=robocup_dir,
        config_path=config_path,
        max_workers=2,
        preprocess_method='SAR'
    ).preprocess_data()
