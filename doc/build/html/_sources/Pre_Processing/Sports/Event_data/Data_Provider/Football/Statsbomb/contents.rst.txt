Statsbomb
==============
.. class:: Event_data(data_provider='statsbomb',event_path=event_path,sb360_path=sb360_path,statsbomb_match_id=statsbomb_match_id,statsbomb_api_args=statsbomb_api_args,max_workers=max_workers).load_data()
    
    Load StatsBomb event and 360 data from files or API. (currently the API freezeframe data is not implemented)

    :param event_path: Path to the JSON file containing the event data.
    :type event_path: str
    :param sb360_path: Path to the JSON file containing the 360 data.
    :type sb360_path: str, optional
    :param statsbomb_match_id: Match ID to fetch the event data from the StatsBomb API.
    :type statsbomb_match_id: str, optional
    :param statsbomb_api_args: Additional arguments to pass to the StatsBomb API.
    :type statsbomb_api_args: tuple
    :param max_workers: Maximum number of workers to use for parallel processing.
    :type max_workers: int, optional
    :return: DataFrame containing the consolidated event and freeze frame data.
    :rtype: pd.DataFrame

    **Example usage for single match**:

    .. code-block:: python

        import pandas as pd
        from preprocessing import Event_data

        event_path = 'path/to/event.json'
        sb360_path = 'path/to/360.json'
        match_id = '12345'
        statsbomb_api_args=['creds = {"user": "input your Statsbomb api user name here", "passwd": "input your Statsbomb api password here"}']

        # Load event data from file
        statsbomb_df=Event_data(data_provider='statsbomb',event_path=event_path).load_data()

        # Load event and 360 data from files
        statsbomb_df=Event_data(data_provider='statsbomb',event_path=event_path,sb360_path=sb360_path).load_data()
        
        # Load event data from API
        statsbomb_df=Event_data(data_provider='statsbomb',statsbomb_match_id=match_id,statsbomb_api_args=statsbomb_api_args).load_data()

        print(statsbomb_df.head())

    **Example usage for multiple matches**:

    .. code-block:: python
        
        import pandas as pd
        from preprocessing import Event_data

        event_folder = 'path/to/event/folder'
        sb360_folder = 'path/to/360/folder'
        match_id = ['12345','67890']
        statsbomb_api_args=['creds = {"user": "input your Statsbomb api user name here", "passwd": "input your Statsbomb api password here"}']

        # Load event data from file
        statsbomb_df=Event_data(data_provider='statsbomb',event_path=event_folder).load_data()

        # Load event and 360 data from files
        statsbomb_df=Event_data(data_provider='statsbomb',event_path=event_folder,sb360_path=sb360_folder).load_data()

        # Load event data from API
        statsbomb_df=Event_data(data_provider='statsbomb',statsbomb_match_id=,statsbomb_api_args=statsbomb_api_args).load_data()

        print(statsbomb_df.head())

    **Details**:

    This function loads StatsBomb event data and optionally 360 freeze frame data from specified file paths or API. The `event_path` is mandatory, while `sb360_path` and `match_id` are optional. The function processes these JSON files or API data and combines their data into a single pandas DataFrame through the following steps:

    1. **Load JSON files**: Parse the event and 360 JSON files if provided.
    2. **Fetch data from API**: If `match_id` is provided, fetch the event data from the StatsBomb API.
    3. **Convert 360 data into a DataFrame**:
       - Extract freeze frame data for teammates and opponents.
       - Flatten and pad the list to ensure consistent structure.
    4. **Extract event details**:
       - Iterate through the event data and extract details such as match ID, time, event type, team, player, start and end coordinates.
       - Match event IDs with 360 data if provided.
    5. **Create the resulting DataFrame**:
       - Define columns for the DataFrame.
       - Convert the list of event details to a DataFrame and return it.

    The returned DataFrame contains the following columns:

    - ``match_id``: Identifier for the match.
    - ``period``: Period of the match in which the event occurred.
    - ``time``: Time of the event.
    - ``minute``: Minute of the event.
    - ``second``: Second of the event.
    - ``event_type``: Primary type of the event.
    - ``event_type_2``: Secondary type of the event, if available.
    - ``team``: Name of the team involved in the event.
    - ``home_team``: Indicator if the team is the home team.
    - ``player``: Name of the player involved in the event.
    - ``start_x``: X-coordinate of the event start position.
    - ``start_y``: Y-coordinate of the event start position.
    - ``end_x``: X-coordinate of the event end position.
    - ``end_y``: Y-coordinate of the event end position.

    If 360 data is provided, the DataFrame also includes:

    - ``h1_teammate, h1_actor, h1_keeper, h1_x, h1_y, ..., h11_teammate, h11_actor, h11_keeper, h11_x, h11_y``: Freeze frame data for each player on the home team.
    - ``a1_teammate, a1_actor, a1_keeper, a1_x, a1_y, ..., a11_teammate, a11_actor, a11_keeper, a11_x, a11_y``: Freeze frame data for each player on the away team.


