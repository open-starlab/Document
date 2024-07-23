DataFactory
==============
.. class:: Event_data(data_provider='datafactory', event_path=datafactory_path).load_data() -> pd.DataFrame
    
    Load the datafactory event data from a JSON file and convert it into a DataFrame.

    :param event_path: Path to the JSON file containing event data.
    :type event_path: str

    :return: DataFrame containing event data with additional columns for analysis.
    :rtype: pd.DataFrame

    **Example**

    .. code-block:: python

        import pandas as pd
        from preprocessing import Event_data

        datafactory_path = 'path/to/event_data.json'
        datafactory_df = Event_data(data_provider='datafactory', event_path=datafactory_path).load_data()
        print(datafactory_df.head())

    **Details**

    This function performs the following steps:

    1. Loads the event data from a JSON file specified by `event_path`.
    2. Extracts match ID and team names.
    3. Iterates over different types of events and individual events within each type.
    4. Extracts various event details such as period, minute, second, event type, team, player, and coordinates.
    5. Converts extracted data into a list of events.
    6. Converts the event list into a DataFrame.
    7. Adds a `seconds` column to the DataFrame by converting minutes and seconds to total seconds.
    8. Reorders the columns and sorts the DataFrame by the `seconds` column.

    The returned DataFrame includes the following columns:

    - ``match_id``: Match identifier
    - ``period``: Period of the match (e.g., first half, second half)
    - ``minute``: Minute of the event
    - ``second``: Second of the event
    - ``seconds``: Total seconds calculated from minute and second
    - ``event_type``: Type of the event
    - ``event_type_2``: Subtype of the event
    - ``team``: Team associated with the event
    - ``player``: Player ID associated with the event
    - ``start_x``: Starting x-coordinate of the event
    - ``start_y``: Starting y-coordinate of the event
    - ``start_z``: Starting z-coordinate of the event (if available)
    - ``end_x``: Ending x-coordinate of the event (if available)
    - ``end_y``: Ending y-coordinate of the event (if available)
    - ``end_z``: Ending z-coordinate of the event (if available)