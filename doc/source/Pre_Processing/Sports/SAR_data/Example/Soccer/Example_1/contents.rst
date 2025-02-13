Download and Preprocess DataStadium Data
=====================================================
This script downloads and preprocesses DataStadium data.

Dependencies
------------

* `os`
* `json`
* `tqdm`
* `pandas`
* `openstarlab_preprocessing`

Usage
-----

.. code-block:: python
    
    import os
    import json
    from tqdm import tqdm
    import pandas as pd
    from statsbombpy import sb

    from preprocessing import SAR_data

    datastadium_dir = "/path/to/data_folder/"
    match_id = "2019091416"
    config_path = "/path/to/preprocess_config.json"

    
    # load datastadium (single file)
    Soccer_SAR_data(
        data_provider='datastadium',
        data_path=datastadium_dir,
        match_id=match_id,
        config_path=config_path,
    ).load_data()

    # load datastadium (multiple files)
    Soccer_SAR_data(
        data_provider='datastadium',
        data_path=datastadium_dir,
        config_path=config_path,
        max_workers=2
    ).load_data()


    # preprocess datastadium (single file)
    Soccer_SAR_data(
        data_provider='datastadium',
        data_path=datastadium_dir,
        match_id=match_id,
        config_path=config_path,
        preprocess_method="SAR"
    ).preprocess_single_data(
        cleaning_dir=os.getcwd()+"/data/dss/clean_data",
        preprocessed_dir=os.getcwd()+"/data/dss/preprocess_data"
    )

    # preprocess datastadium (multiple files)
    Soccer_SAR_data(
        data_provider='datastadium',
        data_path=datastadium_dir,
        config_path=config_path,
        preprocess_method="SAR"
    ).preprocess_multiple_data(
        cleaning_dir=os.getcwd()+"/data/dss/clean_data",
        preprocessed_dir=os.getcwd()+"/data/dss/preprocess_data"
    )

