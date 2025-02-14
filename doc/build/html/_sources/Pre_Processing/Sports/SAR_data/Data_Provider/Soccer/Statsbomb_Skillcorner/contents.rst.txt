Statsbomb with Skillcorner
============================
.. class:: SAR_data(data_provider='statsbomb_skillcorner',statsbomb_event_dir=statsbomb_event_dir,skillcorner_tracking_dir=skillcorner_tracking_dir,skillcorner_match_dir=skillcorner_match_dir,statsbomb_match_id=statsbomb_match_id,skillcorner_match_id=skillcorner_match_id,match_id_df=match_id_df,max_workers=max_workers,preprocess_tracking=False).load_data()

    Load and merge StatsBomb event data with SkillCorner tracking data.

    :param str statsbomb_event_dir: Directory path for StatsBomb event data.
    :param str skillcorner_tracking_dir: Directory path for SkillCorner tracking data.
    :param str skillcorner_match_dir: Directory path for SkillCorner match data.
    :param str statsbomb_match_id: Match ID for StatsBomb data.
    :param str skillcorner_match_id: Match ID for SkillCorner data.
    :param str match_id_df: Path to a CSV file containing match IDs for multiple matches.
    :param int max_workers: Maximum number of workers to use for parallel processing.
    :param bool preprocess_tracking: Whether to preprocess tracking data and event data in to one coordiante system.
    :return: A DataFrame containing the combined event and tracking data.
    :rtype: pd.DataFrame

    **Example usage for single match**:

    .. code-block:: python

        import pandas as pd
        from preprocessing import SAR_data

        statsbomb_event_dir = '/path/to/statsbomb/events'
        skillcorner_tracking_dir = '/path/to/skillcorner/tracking'
        skillcorner_match_dir = '/path/to/skillcorner/match'
        statsbomb_match_id = 'statsbomb_match_id'
        skillcorner_match_id = 'skillcorner_match_id'

        #Load single match data
        statsbomb_skillcorner_df=SAR_data(data_provider='statsbomb_skillcorner',
                                          statsbomb_event_dir=statsbomb_event_dir,
                                          skillcorner_tracking_dir=skillcorner_tracking_dir,
                                          skillcorner_match_dir=skillcorner_match_dir,
                                          statsbomb_match_id=statsbomb_match_id,
                                          skillcorner_match_id=skillcorner_match_id
                                          preprocess_tracking=False #True if you want to preprocess tracking data and event data in to one coordiante system
                                          ).load_data()
        print(statsbomb_skillcorner_df.head())


    **Example usage for multiple matches**:

    .. code-block:: python

        import pandas as pd
        from preprocessing import SAR_data

        statsbomb_event_dir = '/path/to/statsbomb/events'
        skillcorner_tracking_dir = '/path/to/skillcorner/tracking'
        skillcorner_match_dir = '/path/to/skillcorner/match'
        match_id_df = '/path/to/match_id.csv' #(For laliga 23-24 data, lcoated in "openstarlab_preprocessing/open/example/id_matching.csv")

        #Load multiple matches data
        statsbomb_skillcorner_df=SAR_data(data_provider='statsbomb_skillcorner',
                                        statsbomb_event_dir=statsbomb_event_dir,
                                        skillcorner_tracking_dir=skillcorner_tracking_dir,
                                        skillcorner_match_dir=skillcorner_match_dir,
                                        match_id_df=match_id_df,
                                        max_workers=10
                                        preprocess_tracking=False #True if you want to preprocess tracking data and event data in to one coordiante system
                                        ).load_data()
        print(statsbomb_skillcorner_df.head())

    **Details**:

    This function combines event data from StatsBomb and tracking data from SkillCorner for a specific match into a pandas DataFrame:

    1. **File Paths**: Constructs file paths based on provided directories and match IDs.
    2. **Data Loading**: Loads event data from a CSV file (StatsBomb) and tracking data from JSON files (SkillCorner).
    3. **Team Name Mapping**: Maps team names to standard names using a predefined dictionary.
    4. **Player and Ball Tracking**: Extracts and structures player and ball tracking data from SkillCorner data.
    5. **Data Processing**: Iterates through StatsBomb event data, extracts event details, and integrates them with tracking data.
    6. **DataFrame Creation**: Constructs a DataFrame containing event details, team names, player names, event coordinates, and tracking data (if available).
    7. **Sorting**: Sorts events chronologically by 'period', 'minute', and 'second'.

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