Wyscout
==============
.. class:: Event_data(data_provider='wyscout',event_path=event_path ,wyscout_matches_path=wyscout_matches_path,max_workers=max_workers).load_data()

    Load and process Wyscout event data from a JSON file and optionally match data from another JSON file.

    :param event_path: Path to the event JSON file.
    :type event_path: str
    :param wyscout_matches_path: Path to the matches JSON file. Default is None.
    :type wyscout_matches_path: str, optional
    :param max_workers: Maximum number of workers to use for parallel processing. Default is 1.
    :type max_workers: int, optional
    :return: DataFrame containing processed event data.
    :rtype: pd.DataFrame

    **Example usage for single match**:

    .. code-block:: python

        import pandas as pd
        from preprocessing import Event_data

        event_path='path/to/event.json'
        wyscout_matches_path='path/to/matches.json'

        wyscout_df=Event_data(data_provider='wyscout',event_path=event_path ,wyscout_matches_path=wyscout_matches_path).load_data()
        print(wyscout_df.head())

    **Example usage for multiple matches**:

    .. code-block:: python

        from preprocessing import Event_data

        event_folder='path/to/event/folder'
        matches_folder='path/to/matches/folder'

        wyscout_df=Event_data(data_provider='wyscout',
                           event_path=event_folder,
                           wyscout_matches_path=matches_folder,
                           max_workers=10).load_data()
        print(wyscout_df.head())

    **Details**:

    This function reads Wyscout event data from a JSON file and converts it into a DataFrame. It includes the option to
    incorporate match data to identify whether a team is playing at home or away.

    1. **Load JSON files**: Load the event JSON file specified by `event_path` and Optionally load the matches JSON file specified by `matches_path`.
    2. **Process event data**: Extract event details such as match ID, period, seconds, event type, event subtype, accuracy, team ID, player ID, and positional coordinates (start and end). and Categorize events into specific types and sub-types based on predefined criteria for "Shot", "Duel", "Others on the ball", and "Pass" events.
    3. **Match data handling**: If `matches_path` is provided, determine whether the team associated with each event is playing at home or away based on the matches data.
    4. **DataFrame creation**: Convert the processed event data into a Pandas DataFrame with columns i
    5. **Additional column**: Add a column `comp` to the DataFrame indicating the competition name extracted from the `event_path`.

    The returned DataFrame contains the following columns:

    - ``comp``: Name of the competition extracted from the event file path.
    - ``match_id``: Identifier for the match where the event occurred.
    - ``period``: Period or phase of the match when the event took place (e.g., first half, second half, extra time).
    - ``seconds``: Time in seconds when the event occurred within the match.
    - ``event_type``: Primary type of the event (e.g., "Shot", "Duel", "Others on the ball", "Pass").
    - ``event_type_2``: Secondary type of the event, providing additional specificity if available (e.g., "Goal", "Own_goal", "Touch_good", "Ground attacking duel_off dribble").
    - ``accurate``: Boolean indicating if the event was accurate (True) or not (False), typically for events like shots.
    - ``team``: Identifier for the team involved in the event.
    - ``home_team``: Binary indicator (1 or 0) specifying whether the team associated with the event was playing at home (1) or away (0).
    - ``player``: Identifier for the player who performed the event.
    - ``start_x``: X-coordinate of the starting position of the event on the field.
    - ``start_y``: Y-coordinate of the starting position of the event on the field.
    - ``end_x``: X-coordinate of the ending position of the event on the field if applicable (e.g., for passes).
    - ``end_y``: Y-coordinate of the ending position of the event on the field if applicable (e.g., for passes).

