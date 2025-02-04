DataStadium
==============
.. class:: SAR_data(data_provider='datastadium',event_path=play_csv_path, home_tracking_path=home_tracking_csv_path, away_tracking_path=away_tracking_csv_path).load_data() -> pd.DataFrame

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
        from preprocessing import SAR_data

        event_path = 'path/to/play.csv'
        home_tracking_path = 'path/to/home_tracking.csv'
        away_tracking_path = 'path/to/away_tracking.csv'
        
        datastadium_df = SAR_data(
            event_path=event_path, 
            home_tracking_path=home_tracking_path,
            away_tracking_path=away_tracking_path
        ).load_data()
        
        print(datastadium_df.head())

    **Example for mutiple match**

    .. code-block:: python

        import pandas as pd
        from preprocessing import SAR_data

        data_dir = 'path/to/data/dir' #the dir contain folders that contain the play.csv and tracking.csv files
        
        datastadium_df = SAR_data(
            event_path=data_dir
        ).load_data()
        
        print(datastadium_df.head())

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

    The returned DataFrame consists of event and tracking data.
    The event data includes the following columns:
    - ``match_id (int)``: Unique identifier for each match.
    - ``frame_id (int)``: Unique identifier for each frame within a match.
    - ``team (str)``: The team associated with the event.
    - ``team_id (int)``: Unique identifier for each team.
    - ``home_team (int)``: Indicator of whether the team is the home team (1: home, 0: away).
    - ``player_name (str)``: The player associated with the event.
    - ``player_id (int)``: Unique identifier for each player.
    - ``jersey_number (int)``: The player jersey number associated with the event.
    - ``player_role (int)``: The identifier for each position of each player (1: GK, 2: DF, 3: MF, 4: FW).
    - ``action (str)``: Simplified and standardized description of the event action.
    - ``action_id (int)``: Unique identifier for each event action.
    - ``success (int)``: Indicator of whether the event action was successful (1: success, 0: failure).
    - ``is_goal (int)``: Indicator of whether the event resulted in a goal (1: goal, 0: no goal).
    - ``is_shot (int)``: Indicator of whether the event is a shot (1: shot, 0: no shot).
    - ``is_pass (int)``: Indicator of whether the event is a pass (1: pass, 0: no pass).
    - ``is_dribble (int)``: Indicator of whether the event is a dribble (1: dribble, 0: no dribble).
    - ``is_cross (int)``: Indicator of whether the event is a cross (1: cross, 0: no cross).
    - ``is_through (int)``: Indicator of whether the event is a through (1: through, 0: no through).
    - ``is_ball_recovery (int)``: Indicator of whether the event is a ball_recovery (1: ball_recovery, 0: no ball_recovery).
    - ``is_block (int)``: Indicator of whether the event is a block (1: block, 0: no block).
    - ``is_clearance (int)``: Indicator of whether the event is a clearance (1: clearance, 0: no clearance).
    - ``is_interception (int)``: Indicator of whether the event is a interception (1: interception, 0: no interception).
    - ``Period (int)``: The period of the match (1: 1st half, 2: 2nd half, etc.).
    - ``seconds (float)``: The total seconds elapsed since the start of the match, adjusted for different periods.
    - ``start_x (float)``: The x-coordinate of the player location when event's starting (scaled).
    - ``start_y (float)``: The y-coordinate of the player location when event's starting (scaled).
    - ``ball_y (float)``: The x-coordinate of the ball location when event's starting (scaled).
    - ``ball_y (float)``: The y-coordinate of the ball location when event's starting (scaled).
    - ``ball_touch (int)``: Only event valid as play $1$ Ball out, fouls, etc. $0$.
    - ``series_num (int)``: Sequential number of the sequence of in-play of the match.
    - ``history_num (int)``: No. of the history in chronological order of the play of the match (the start of the match is $1$, and after that, the number is $1+$ or higher than the previous history No.).
    - ``attack_history_num (int)``: Number for asingle series of attack.
    - ``attack_start_num (int)``: First history No. within the same attack_history_num.
    - ``attack_end_num (int)``: Last history No. within the same attack_history_num.


    The tracking data includes the following columns:
    - ``match_id (int)``: Unique identifier for each match.
    - ``frame_id (int)``: Unique identifier for each frame within a match.
    - ``home_team (int)``: Indicator of whether the team is the home team (1: home, 0: away).
    - ``jersey_number (int)``: The player jersey number associated with the event.
    - ``x (float)``: The x-coordinate of the player location scale by the field size.
    - ``y (float)``: The y-coordinate of the player location scale by the field size.
