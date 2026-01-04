Robocup 2D simulation
=====================

.. class:: Event_data(data_provider='robocup_2d',event_path=event_path,match_id=match_id,tracking_path=tracking_path).load_data()

    Loads RoboCup 2D event data from a CSV file and optionally merges it with tracking data.

    :param event_path: Path to the CSV file containing event data.
    :type event_path: str
    :param match_id: Identifier for the match. Defaults to None.
    :type match_id: str, optional
    :param tracking_path: Path to the CSV file containing tracking data. Defaults to None.
    :type tracking_path: str, optional
    :return: A DataFrame containing event and tracking data.
    :rtype: pd.DataFrame

    **Example usage**:

    .. code-block:: python

        import pandas as pd
        from preprocessing import Event_data

        event_path = 'path/to/event_data.csv'
        tracking_path = 'path/to/tracking_data.csv'
        match_id = 'match_123'

        # Load event data only
        robocup_2d_df=Event_data(data_provider='robocup_2d',event_path=event_path,match_id=match_id).load_data()

        # Load event data and merge with tracking data
        robocup_2d_df=Event_data(data_provider='robocup_2d',event_path=event_path,match_id=match_id,tracking_path=tracking_path).load_data()
        print(robocup_2d_df.head())

    **Details**:

    This function loads event data from the specified CSV file and optionally merges it with tracking data if a tracking path is provided. The data is then organized into a pandas DataFrame through the following steps:

    * Extracted data from C++ code: https://github.com/helios-base/librcsc/blob/master/src/rcg2csv.cpp
    1. Load event data from the CSV file specified by `event_path`.
    2. If `tracking_path` is provided, load tracking data from the CSV file specified by `tracking_path`.
    3. Define columns for the resulting DataFrame. If tracking data is provided, additional columns for tracking data are included.
    4. Initialize an empty list to store event details.
    5. Iterate through the event records:
       - Extract event details such as time, event type, outcome, team, player, start coordinates, and end coordinates.
       - If tracking data is provided, merge the event details with the corresponding tracking data based on the time (seconds).
    6. Convert the list of event details to a DataFrame.
    7. Sort the DataFrame by the 'seconds' column.
    8. Return the resulting DataFrame.

    The returned DataFrame contains the following columns:

    - ``match_id``: Identifier for the match.
    - ``seconds``: Time in seconds from the start of the match.
    - ``event_type``: Type of the event.
    - ``outcome``: Outcome of the event.
    - ``team``: Team associated with the event.
    - ``player``: Player associated with the event.
    - ``start_x``: Starting x-coordinate of the event on the pitch.
    - ``start_y``: Starting y-coordinate of the event on the pitch.
    - ``end_x``: Ending x-coordinate of the event on the pitch.
    - ``end_y``: Ending y-coordinate of the event on the pitch.

    If tracking data is provided, the DataFrame also includes:

    - ``l_score``: Score of the left team.
    - ``r_score``: Score of the right team.
    - ``b_x``: x-coordinate of the ball.
    - ``b_y``: y-coordinate of the ball.
    - ``l1_x, l1_y, ..., l11_x, l11_y``: Coordinates of the left team players.
    - ``r1_x, r1_y, ..., r11_x, r11_y``: Coordinates of the right team players.