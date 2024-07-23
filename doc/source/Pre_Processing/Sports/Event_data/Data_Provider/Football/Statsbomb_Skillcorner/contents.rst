Statsbomb with Skillcorner
============================
.. class:: Event_data(data_provider='statsbomb_skillcorner',statsbomb_event_dir=statsbomb_event_dir,skillcorner_tracking_dir=skillcorner_tracking_dir,skillcorner_match_dir=skillcorner_match_dir,statsbomb_match_id=statsbomb_match_id,skillcorner_match_id=skillcorner_match_id,match_id_df=match_id_df,max_workers=max_workers).load_data()

    Load and merge StatsBomb event data with SkillCorner tracking data.

    :param str statsbomb_event_dir: Directory path for StatsBomb event data.
    :param str skillcorner_tracking_dir: Directory path for SkillCorner tracking data.
    :param str skillcorner_match_dir: Directory path for SkillCorner match data.
    :param str statsbomb_match_id: Match ID for StatsBomb data.
    :param str skillcorner_match_id: Match ID for SkillCorner data.
    :param str match_id_df: Path to a CSV file containing match IDs for multiple matches.
    :param int max_workers: Maximum number of workers to use for parallel processing.
    :return: A DataFrame containing the combined event and tracking data.
    :rtype: pd.DataFrame

    **Example usage for single match**:

    .. code-block:: python

        import pandas as pd
        from preprocessing import Event_data

        statsbomb_event_dir = '/path/to/statsbomb/events'
        skillcorner_tracking_dir = '/path/to/skillcorner/tracking'
        skillcorner_match_dir = '/path/to/skillcorner/match'
        statsbomb_match_id = 'statsbomb_match_id'
        skillcorner_match_id = 'skillcorner_match_id'

        #Load single match data
        statsbomb_skillcorner_df=Event_data(data_provider='statsbomb_skillcorner',
                                          statsbomb_event_dir=statsbomb_event_dir,
                                          skillcorner_tracking_dir=skillcorner_tracking_dir,
                                          skillcorner_match_dir=skillcorner_match_dir,
                                          statsbomb_match_id=statsbomb_match_id,
                                          skillcorner_match_id=skillcorner_match_id
                                          ).load_data()
        print(statsbomb_skillcorner_df.head())


    **Example usage for multiple matches**:

    .. code-block:: python

        import pandas as pd
        from preprocessing import Event_data

        statsbomb_event_dir = '/path/to/statsbomb/events'
        skillcorner_tracking_dir = '/path/to/skillcorner/tracking'
        skillcorner_match_dir = '/path/to/skillcorner/match'
        match_id_df = '/path/to/match_id.csv' #(For laliga 23-24 data, lcoated in "openstarlab_preprocessing/open/example/id_matching.csv")

        #Load multiple matches data
        statsbomb_skillcorner_df=Event_data(data_provider='statsbomb_skillcorner',
                                        statsbomb_event_dir=statsbomb_event_dir,
                                        skillcorner_tracking_dir=skillcorner_tracking_dir,
                                        skillcorner_match_dir=skillcorner_match_dir,
                                        match_id_df=match_id_df,
                                        max_workers=10).load_data()
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

    The returned DataFrame contains the following columns:

    - ``match_id``: Identifier for the match.
    - ``period``: Period of the match when the event occurred (e.g., 1st half, 2nd half).
    - ``time``: Exact timestamp when the event occurred (HH:MM:SS).
    - ``minute``: Minute of the match when the event occurred.
    - ``second``: Second of the match when the event occurred.
    - ``seconds``: Total seconds elapsed in the match at the time of the event.
    - ``event_type``: Primary type of the event (e.g., "Pass", "Shot", "Foul").
    - ``event_type_2``: Secondary type of the event, providing additional context if available (e.g., "Corner" for passes, outcome of a shot).
    - ``team``: Name of the team involved in the event.
    - ``home_team``: Binary indicator (1 or 0) denoting whether the team is the home team (1) or away team (0).
    - ``player``: Name of the player involved in the event.
    - ``start_x``: X-coordinate of the event start position on the field.
    - ``start_y``: Y-coordinate of the event start position on the field.
    - ``end_x``: X-coordinate of the event end position on the field (if applicable, e.g., for passes or shots).
    - ``end_y``: Y-coordinate of the event end position on the field (if applicable, e.g., for passes or shots).

    If tracking data is available, the DataFrame will also include:

    - ``h1_x, h1_y, ..., h16_x, h16_y``: X and Y coordinates for each player on the home team (indexed from h1 to h16).
    - ``a1_x, a1_y, ..., a16_x, a16_y``: X and Y coordinates for each player on the away team (indexed from a1 to a16).

    The tracking data provides positional information for each player during specific moments of the match, allowing for detailed analysis and visualization of player movements and interactions throughout the game.

