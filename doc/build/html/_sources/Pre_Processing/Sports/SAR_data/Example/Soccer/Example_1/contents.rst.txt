Download and Preprocess DataStadium Data
=====================================================
This script downloads and preprocesses DataStadium data.

Dependencies
------------

* `openstarlab_preprocessing`

Usage
-----

.. code-block:: python

    from preprocessing import SAR_data

    datastadium_dir = "/path/to/data_folder/"
    state_def = "PVS"
    match_id = "2019091416"
    config_path = "/path/to/preprocess_config.json"

    
    # load and preprocess datastadium (single file)
    Soccer_SAR_data(
        data_provider='datastadium',
        state_def=state_def,
        data_path=datastadium_dir,
        match_id=match_id,
        config_path=config_path,
        preprocess_method='SAR'
    ).preprocess_data()

    # load and preprocess datastadium (multiple files)
    Soccer_SAR_data(
        data_provider='datastadium',
        state_def=state_def,
        data_path=datastadium_dir,
        config_path=config_path,
        max_workers=2,
        preprocess_method='SAR'
    ).preprocess_data()

