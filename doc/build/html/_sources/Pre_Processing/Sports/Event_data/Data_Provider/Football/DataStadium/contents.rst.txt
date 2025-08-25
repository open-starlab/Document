DataStadium
==============
.. class:: Event_data(data_provider='datastadium',event_path=play_csv_path, home_tracking_path=home_tracking_csv_path, away_tracking_path=away_tracking_csv_path).load_data() -> pd.DataFrame

    Load and process stadium event and tracking data from CSV files and convert it into a DataFrame.

    :param event_path: Path to the play CSV file containing event data.
    :type event_path: str
    :param home_tracking_path: Path to the home_tracking CSV file containing home team tracking data.
    :type home_tracking_path: str
    :param away_tracking_path: Path to the away_tracking CSV file containing away team tracking data.
    :type away_tracking_path: str

    :return: DataFrame containing merged and processed event and tracking data.
    :rtype: pd.DataFrame

    .. note::

        The `DataStadium` tracking data data requires preprocessing. Which could be handled with the `Tracking_data` class. Ensure this preprocessing step is completed before using this function.

        For more details, refer to the `Tracking_data` class documentation: 
        `process_datadium_tracking_data Documentation <https://openstarlab.readthedocs.io/en/latest/Pre_Processing/Sports/Tracking_data/Data_Provider/Football/DataStadium/contents.html>`_

    **Example for single match**

    .. code-block:: python

        import pandas as pd
        from preprocessing import Event_data

        event_path = 'path/to/play.csv'
        home_tracking_path = 'path/to/home_tracking.csv'
        away_tracking_path = 'path/to/away_tracking.csv'
        
        stadium_df = Event_data(
            event_path=event_path, 
            home_tracking_path=home_tracking_path,
            away_tracking_path=away_tracking_path
        ).load_data()
        
        print(stadium_df.head())

    **Example for mutiple match**

    .. code-block:: python

        import pandas as pd
        from preprocessing import Event_data

        data_dir = 'path/to/data/dir' #the dir contain folders that contain the play.csv and tracking.csv files
        
        stadium_df = Event_data(
            event_path=data_dir
        ).load_data()
        
        print(stadium_df.head())

    **Details**

    This function performs the following steps:

    1. Loads the event data from the CSV file specified by `event_path`.
    2. Loads the home and away team tracking data from the CSV files specified by `home_tracking_path` and `away_tracking_path`.
    3. Filters and preprocesses the event data by retaining required columns and sorting by absolute time.
    4. Creates a new column `event_type_2` based on event flags.
    5. Renames columns to standardized names and reorders them.
    6. Converts event types to English using predefined dictionaries.
    7. Calculates the period, minute, and second for each event based on absolute time.
    8. Appends tracking data to the event data by aligning timestamps.
    9. Creates and returns a final DataFrame with event and tracking data.

    The returned DataFrame includes the following columns:

    - ``match_id``: Match identifier
    - ``Period``: Period of the match (e.g., first half, second half)
    - ``Minute``: Minute of the event
    - ``Second``: Second of the event
    - ``frame``: Frame number of the event
    - ``absolute_time``: Absolute time in seconds
    - ``team``: Team associated with the event
    - ``home``: Home or away team indicator
    - ``player``: Player ID associated with the event
    - ``event_type``: Type of the event
    - ``event_type_2``: Subtype of the event
    - ``success``: Success flag of the event
    - ``start_x``: Starting x-coordinate of the event
    - ``start_y``: Starting y-coordinate of the event
    - ``dist``: Distance associated with the event
    - ``opp_field``: Indicator for opponent's field
    - ``point_diff``: Difference in points
    - ``self_score``: Self team score
    - ``opp_score``: Opponent's score
    - ``angle2goal``: Angle to goal
    - ``dist2goal``: Distance to goal

    The DataFrame also includes tracking data columns for both home and away teams, such as ``Home_1_x``, ``Home_1_y``, ``Away_1_x``, and ``Away_1_y``.