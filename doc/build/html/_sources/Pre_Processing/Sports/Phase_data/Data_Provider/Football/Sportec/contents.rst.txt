Sportec
==============
.. class:: Event_data(data_provider='sportec', event_path=event_path, tracking_path=tracking_path, meta_data=meta_path).load_data()

    Load Sportec event, tracking, and meta data from XML files into a pandas DataFrame.

    :param event_path: Path to the event XML file.
    :type event_path: str
    :param tracking_path: Path to the tracking XML file. Defaults to None.
    :type tracking_path: str, optional
    :param meta_path: Path to the meta XML file. Defaults to None.
    :type meta_path: str, optional
    :return: A DataFrame containing the combined event, tracking, and meta data.
    :rtype: pd.DataFrame

    **Example usage**:

    .. code-block:: python

        import pandas as pd
        from preprocessing import Event_data

        event_path = 'path/to/event.xml'
        tracking_path = 'path/to/tracking.xml'
        meta_path = 'path/to/meta.xml'

        # Load event data only
        sportec_df = Event_data(data_provider='sportec', event_path=event_path).load_data()

        # Load event data and merge with tracking and meta data
        sportec_df = Event_data(data_provider='sportec', event_path=event_path, tracking_path=tracking_path, meta_data=meta_path).load_data()

        print(sportec_df.head())

    **Details**:

    This function loads data from three types of XML files: event, tracking, and meta data. The `event_path` is mandatory, while `tracking_path` and `meta_path` are optional. The function processes these XML files and combines their data into a single pandas DataFrame through the following steps:

    1. **Load XML files**: Parse the event, tracking, and meta XML files.
    2. **Create dictionaries for team and player information**:
       - Extract team information from the meta XML file and store it in a dictionary.
       - Extract player information from the meta XML file and store it in a dictionary.
    3. **Initialize an empty list to store event details**.
    4. **Iterate through each event**:
       - Extract event details such as match ID, time, event type, outcome, team, player, start and end coordinates.
       - Replace team and player IDs with their names using the dictionaries created earlier.
       - If tracking data is provided, merge the event details with the corresponding tracking data based on the time.
    5. **Define columns for the resulting DataFrame**:
       - Basic columns for event data.
       - Additional columns for tracking data if provided.
    6. **Convert the list of event details to a DataFrame** and return it.

    The returned DataFrame contains the following columns:

    - ``match_id``: Identifier for the match.
    - ``time``: Time of the event.
    - ``event_type``: Primary type of the event.
    - ``event_type_2``: Secondary type of the event, if available.
    - ``outcome``: Outcome of the event.
    - ``team``: Name of the team involved in the event.
    - ``player``: Name of the player involved in the event.
    - ``start_x``: X-coordinate of the event start position.
    - ``start_y``: Y-coordinate of the event start position.
    - ``end_x``: X-coordinate of the event end position.
    - ``end_y``: Y-coordinate of the event end position.

    If tracking data is provided, the DataFrame also includes:

    - ``h1_x, h1_y, h1_z, ..., h16_x, h16_y, h16_z``: Coordinates for each player on the home team.
    - ``a1_x, a1_y, a1_z, ..., a16_x, a16_y, a16_z``: Coordinates for each player on the away team.


