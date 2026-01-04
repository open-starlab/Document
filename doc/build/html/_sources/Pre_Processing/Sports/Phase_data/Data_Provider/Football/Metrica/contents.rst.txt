Metrica
==============
.. class:: Event_data(data_provider='metrica',event_path=metrica_event_csv_path,match_id=match_id,tracking_home_path=metrica_tracking_home_path,tracking_away_path=metrica_tracking_away_path).load_data()

    Loads event data and tracking data from specified file paths and returns a DataFrame containing the merged information.

    :param event_path: Path to the JSON or CSV file containing event data.
    :type event_path: str
    :param match_id: ID of the match. Default is None.
    :type match_id: str, optional
    :param tracking_home_path: Path to the CSV file containing home team tracking data. Default is None.
    :type tracking_home_path: str, optional
    :param tracking_away_path: Path to the CSV file containing away team tracking data. Default is None.
    :type tracking_away_path: str, optional
    :returns: A DataFrame containing the event data along with the extracted details, optionally including tracking data.
    :rtype: pd.DataFrame

    **Example usage**:

    .. code-block:: python

        import pandas as pd
        from preprocessing import Event_data

        event_path = 'path/to/event_data.json'
        match_id = '12345'
        tracking_home_path = 'path/to/home_tracking.csv'
        tracking_away_path = 'path/to/away_tracking.csv'

        #Without tracking data
        metrica_df = Event_data(data_provider='metrica',event_path=metrica_event_csv_path,match_id=match_id).load_data()

        #With tracking data
        metrica_df = Event_data(data_provider='metrica',event_path=metrica_event_csv_path,match_id=match_id,
                           tracking_home_path=metrica_tracking_home_path,tracking_away_path=metrica_tracking_away_path).load_data()
        print(metrica_df.head())

    **Details**:

    The function performs the following steps:

    1. Loads event data from the specified JSON or CSV file.
    2. Optionally loads home and away team tracking data from CSV files if provided.
    3. Processes and merges the event data with tracking data.
    4. Returns a pandas DataFrame containing the combined event and tracking data.

    The returned DataFrame includes the following columns:

    - ``match_id``: ID of the match.
    - ``period``: Period of the match.
    - ``seconds``: Time in seconds when the event occurred.
    - ``frame``: Frame number when the event occurred.
    - ``event_type``: Type of event.
    - ``event_type_2``: Subtype of event.
    - ``team``: Name of the team involved in the event.
    - ``player``: Name of the player involved in the event.
    - ``start_x``: Starting X coordinate of the event.
    - ``start_y``: Starting Y coordinate of the event.
    - ``end_x``: Ending X coordinate of the event.
    - ``end_y``: Ending Y coordinate of the event.
    - ``h{i}_x, h{i}_y``: Coordinates of the home team players (if tracking data is provided).
    - ``a{i}_x, a{i}_y``: Coordinates of the away team players (if tracking data is provided).

    The DataFrame is sorted by the "seconds" column in ascending order.