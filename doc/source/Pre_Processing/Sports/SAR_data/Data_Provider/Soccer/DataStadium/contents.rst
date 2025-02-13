DataStadium
==============
.. class:: SAR_data(data_provider='datastadium', data_path=datastadium_path, match_id=match_id, config_path=config_path).load_data() -> pd.DataFrame

    Load and process stadium event and tracking data from CSV files and convert it into a DataFrame.

    :param data_path: Path to the folder containing the event data and tracking data CSV files.
    :type event_path: str
    :param match_id: The ID of the match. Defaults to None.
    :type home_tracking_path: str
    :param config_path: The path to the configuration file.
    :type away_tracking_path: str

    .. note::

        The `DataStadium` tracking data data requires preprocessing. Which could be handled with the `Tracking_data` class. Ensure this preprocessing step is completed before using this function.

        For more details, refer to the `Tracking_data` class documentation: 
        `process_datadium_tracking_data Documentation <https://openstarlab.readthedocs.io/en/latest/Pre_Processing/Sports/Tracking_data/Data_Provider/Football/DataStadium/contents.html>`_

    **Example for single match**

    .. code-block:: python

        import pandas as pd
        from preprocessing import SAR_data

        datastadium_path = "/path/to/data_folder/"
        match_id = "match_id"
        config_path = "/path/to/preprocess_config.json"

        SAR_data(
            data_provider='datastadium',
            data_path=datastadium_path,
            match_id=match_id,
            config_path=config_path
        ).load_data()

    **Example for mutiple match**

    .. code-block:: python

        import pandas as pd
        from preprocessing import SAR_data

        datastadium_path = "/path/to/data_folder/"
        config_path = "/path/to/preprocess_config.json"

        Soccer_SAR_data(
            data_provider='datastadium',
            data_path=datastadium_path,
            config_path=config_path,
            max_workers=2
        ).load_data()

    **Details**

    This function performs the following steps:

    1. Loads the event data from the CSV file specified by  `data_path/event_data`.
    2. Checks and renames the event columns to standardized names.
    3. Gets the changed player list separated by the team.
    4. Loads the player data from the CSV file specified by `data_path/player_path`.
    5. Checks and renames the player columns.
    6. Loads the home and away team tracking data from the CSV files specified by `data_path/home_tracking_path` and `data_path/away_tracking_path`.
    7. Splits the tracking data into player and ball tracking data.
    8. Checks and renames the player and ball tracking columns.
    9. Interpolates the ball tracking data.
    10. Merges the player and ball tracking data.
    11. Interpolates the player tracking data.
    12. Calculates the player and ball velocity and acceleration.
    13. Merges the event data with the tracking data.
    14. Saves the processed data to a CSV file.

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
