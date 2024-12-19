DataStadium
==============

.. class:: Tracking_data('soccer').process_tracking_data(game_id, data_path, event_data_name="play.csv", player_data_name="player.csv", tracking_data_name1="tracking_1stHalf.csv", tracking_data_name2="tracking_2ndHalf.csv")-> tuple

    Process and load tracking data for a specific game, including tracking data for home and away teams, as well as jersey numbers.

    :param game_id: Index of the game folder in the dataset to process.
    :type game_id: int
    :param data_path: Path to the folder containing the game data.
    :type data_path: str
    :param event_data_name: Name of the event data file. Default is "play.csv".
    :type event_data_name: str, optional
    :param player_data_name: Name of the player data file. Default is "player.csv".
    :type player_data_name: str, optional
    :param tracking_data_name1: Name of the first-half tracking data file. Default is "tracking_1stHalf.csv".
    :type tracking_data_name1: str, optional
    :param tracking_data_name2: Name of the second-half tracking data file. Default is "tracking_2ndHalf.csv".
    :type tracking_data_name2: str, optional

    :return: Tuple containing processed tracking data for the home and away teams, and a DataFrame with jersey numbers of players.
    :rtype: tuple
        - tracking_home (pd.DataFrame): Processed tracking data for the home team.
        - tracking_away (pd.DataFrame): Processed tracking data for the away team.
        - jerseynum_df (pd.DataFrame): DataFrame containing jersey numbers of players.

    **Example for single match**

    .. code-block:: python

        import pandas as pd
        from preprocessing import Tracking_data

        data_path = 'path/to/data/folder'
        game_id = 0
        
        tracking_home, tracking_away, jerseynum_df = Tracking_data('soccer').process_datadium_tracking_data(game_id,data_path)
        
        print(tracking_home.head())
        print(tracking_away.head())
        print(jerseynum_df.head())

    **Example for multiple matches**

    .. code-block:: python

        import pandas as pd
        from preprocessing import Tracking_data

        data_path = 'path/to/data/folder'
        
        for game_id in range(len(os.listdir(data_path))):
            tracking_home, tracking_away, jerseynum_df = Tracking_data('soccer').process_datadium_tracking_data(game_id,data_path)
            print(tracking_home.head())
            print(tracking_away.head())
            print(jerseynum_df.head())

    **Details**

    This function performs the following steps:

    1. Loads the event, player, and tracking data from the specified CSV files.
    2. Sorts the game data by date and processes the event and player data.
    3. Splits the tracking data into home and away team data for both halves of the game.
    4. Extracts unique player jersey numbers for both home and away teams.
    5. Prepares the tracking data for both teams by calculating frame information and periods.
    6. Aligns the tracking data with the corresponding game period and time.
    7. Iterates over the tracking data to fill in player and ball positions at each frame.
    8. Returns the processed tracking data for the home and away teams, as well as a DataFrame with the jersey numbers.

    The returned tuple includes:

    - ``tracking_home``: DataFrame with processed tracking data for the home team, including columns like ``Home_1_x``, ``Home_1_y``, etc.
    - ``tracking_away``: DataFrame with processed tracking data for the away team, including columns like ``Away_1_x``, ``Away_1_y``, etc.
    - ``jerseynum_df``: DataFrame with player jersey numbers for both teams, including columns like ``Player_ID``, ``Team``, ``Jersey_Number``.
