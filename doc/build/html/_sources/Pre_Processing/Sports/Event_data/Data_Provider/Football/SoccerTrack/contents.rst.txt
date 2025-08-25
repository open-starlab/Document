BePro
==============
.. class:: Event_data(data_provider='bepro', event_path=event_path, st_track_path=st_track_path, st_meta_path=st_meta_path, verbose=False).load_data() -> pd.DataFrame

   Load and process event and tracking data for the SoccerTrackv2 dataset (BePro data).

   :param event_path: Path to the CSV file containing event data.
   :type event_path: str
   :param st_track_path: Path to the XML file containing tracking data.
   :type st_track_path: str
   :param st_meta_path: Path to the XML file containing match metadata (pitch dimensions, teams, players, etc.).
   :type st_meta_path: str
   :param verbose: If True, prints additional information about the merging process and feature extraction. Defaults to False.
   :type verbose: bool, optional
   :returns: A DataFrame containing the merged and processed event and tracking data.
   :rtype: pandas.DataFrame

   **Example usage**:

   .. code-block:: python

        import pandas as pd
        from preprocessing import Event_data

        event_path = 'path/to/event.csv'
        tracking_path = 'path/to/tracking.xml'
        meta_path = 'path/to/meta.xml'

        # Load and process soccer data
        soccertrack_df = Event_data('bepro',event_path, 
                                          st_track_path = tracking_path, 
                                          st_meta_path = meta_path).load_data()
        print(soccertrack_df.head())

   **Details**:

   This function combines event data with tracking data by merging based on event time. It also adds
   additional features extracted from metadata, such as player information, and converts position
   coordinates to the correct scale for analysis. The function performs the following steps:

   1. Loads the event data from a CSV file.
   2. Reads tracking data from an XML file.
   3. Extracts metadata (pitch information, team information, player information) from an XML file.
   4. Adds additional features to the event data.
   5. Merges tracking data with event data based on the nearest time match.
   6. Adds player-specific features for both home and away teams.
   7. Adds ball-specific features.

   The returned DataFrame contains the following columns:

   - ``event_time``: Time of the event in milliseconds.
   - ``event_period``: Period of the match (e.g., "FIRST_HALF", "SECOND_HALF").
   - ``team_id``: ID of the team involved in the event.
   - ``player_id``: ID of the player involved in the event.
   - ``x``, ``y``: Scaled coordinates of the event on the pitch.
   - ``event_types``: Types of the event.
   - ``period``: Numerical representation of the match period (1 for first half, 2 for second half, etc.).
   - ``seconds``: Time of the event in seconds.
   - ``event_type``: Primary type of the event.
   - ``home_team``: Binary indicator (1 for home team, 0 for away team).
   - ``x_unscaled``, ``y_unscaled``: Unscaled coordinates of the event on the pitch.
   - ``tracking_time``: The matchTime of the synced tracking data in milliseconds.

   For each player (both home and away teams):

   - ``{home/away}_player_id_{n}``: ID of the nth player.
   - ``{home/away}_x_{n}``, ``{home/away}_y_{n}``: Coordinates of the nth player.
   - ``{home/away}_speed_{n}``: Speed of the nth player.
   - ``{home/away}_name_{n}``: Name of the nth player.
   - ``{home/away}_nameEn_{n}``: English name of the nth player.
   - ``{home/away}_shirtNumber_{n}``: Shirt number of the nth player.
   - ``{home/away}_position_{n}``: Position of the nth player.

   For the ball:

   - ``ball_x``, ``ball_y``: Coordinates of the ball.
   - ``ball_speed``: Speed of the ball.

   Note: The x,y coordinates is fixed regardless of the attacking direction.


