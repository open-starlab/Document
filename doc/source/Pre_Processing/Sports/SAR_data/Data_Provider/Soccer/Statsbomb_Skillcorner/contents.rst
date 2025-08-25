Statsbomb with Skillcorner
============================
.. class:: Soccer_SAR_data(data_provider='statsbomb_skillcorner', state_def=state_def, data_path=statsbomb_skillcorner_path, match_id="1120811", config_path=config_path, statsbomb_skillcorner_match_id=statsbomb_skillcorner_match_id, preprocess_method='SAR').preprocess_data()

    Load, merge and process StatsBomb event data with SkillCorner tracking data.

    :param state_def: The state definition to use for preprocessing.
    :type state_def: str
    :param data_path: Directory path for StatsBomb and SkillCorner data.
    :type data_path: str
    :param match_id: Match ID for SkillCorner data.
    :type match_id: str
    :param config_path: Path to the configuration file.
    :type config_path: str
    :param statsbomb_skillcorner_match_id: Path to a CSV file containing match IDs for multiple matches.
    :type statsbomb_skillcorner_match_id: str
    :param preprocess_method: The preprocessing method to use. Defaults to None.
    :type preprocess_method: str

    **Example usage for single match**:

    .. code-block:: python

        import pandas as pd
        from preprocessing import SAR_data

        data_path = '/path/to/statsbomb_skillcorner'
        state_def = 'PVS'
        match_id = 'match_id'
        config_path = '/path/to/preprocess_config.json'
        statsbomb_skillcorner_match_id = '/path/to/statsbomb_skillcorner_match_id.json'

        #Load single match data
        Soccer_SAR_data(
            data_provider='statsbomb_skillcorner',
            state_def=state_def,
            data_path=data_path,
            match_id=match_id, # match_id for skillcorner
            config_path=config_path,
            statsbomb_skillcorner_match_id=statsbomb_skillcorner_match_id,
            preprocess_method='SAR'
        ).preprocess_method()


    **Example usage for multiple matches**:

    .. code-block:: python

        import pandas as pd
        from preprocessing import SAR_data

        data_path = '/path/to/statsbomb_skillcorner'
        state_def = 'PVS'
        config_path = '/path/to/preprocess_config.json'
        statsbomb_skillcorner_match_id = '/path/to/statsbomb_skillcorner_match_id.json'

        #Load multiple matches data
        Soccer_SAR_data(
            data_provider='statsbomb_skillcorner',
            state_def=state_def,
            data_path=data_path,
            config_path=config_path,
            statsbomb_skillcorner_match_id=statsbomb_skillcorner_match_id,
            max_workers=2,
            preprocess_method='SAR'
        ).preprocess_data()

    **Details**:

    This function combines event data from StatsBomb and tracking data from SkillCorner for a specific match into a pandas DataFrame:

    1. **File Paths**: Constructs file paths based on provided directories and match IDs.
    2. **Data Loading**: Loads event data from a CSV file (StatsBomb) and tracking data from JSON files (SkillCorner).
    3. **Team Name Mapping**: Maps team names to standard names using a predefined dictionary.
    4. **Player and Ball Tracking**: Extracts and structures player and ball tracking data from SkillCorner data.
    5. **Data Processing**: Iterates through StatsBomb event data, extracts event details, and integrates them with tracking data.
    6. **DataFrame Creation**: Constructs a DataFrame containing event details, team names, player names, event coordinates, and tracking data (if available).
    7. **Sorting**: Sorts events chronologically by 'period', 'minute', and 'second'.
    8. **Spliting Data Structures**: Splits the event and tracking data into play.csv (event data), player.csv (player tracking data), ball.csv (ball tracking data), and players.csv (player metadata).
    9. **Cleaning Data**: Removes unnecessary columns and standardizes column names.
    10. **Interpolating Data**: Interpolates missing tracking data.
    11. **Saving Data**: Saves the processed data to a CSV file.

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