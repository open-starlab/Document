Download and Preprocess FIFAWorldCup Data
=====================================================
This script downloads and preprocesses FIFAWorldCup data.

Dependencies
------------

* `openstarlab_preprocessing`

Usage
-----

.. code-block:: python

    from preprocessing import SAR_data

    fifawc_dir = "/path/to/data_folder/"
    state_def = "PVS"
    match_id = "3812"
    config_path = "/path/to/preprocess_config.json"

    
    # load and preprocess fifawc (single file)
    Soccer_SAR_data(
        data_provider='fifawc',
        state_def=state_def,
        data_path=fifawc_dir,
        match_id=match_id,
        config_path=config_path,
        preprocess_method='SAR'
    ).preprocess_data()

    # load and preprocess fifawc (multiple files)
    Soccer_SAR_data(
        data_provider='fifawc',
        state_def=state_def,
        data_path=fifawc_dir,
        config_path=config_path,
        max_workers=2,
        preprocess_method='SAR'
    ).preprocess_data()

