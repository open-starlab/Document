PFF FC
==============
.. class:: Event_data(data_provider='pff_fc', event_path=event_path ,max_workers=max_workers).load_data()

    Load and process PFF FC event data from a JSON file or folder.

    :param event_path: Path to the event JSON files/Folder.
    :param max_workers: Maximum number of workers to use for parallel processing. Default is 1.
    :type max_workers: int, optional
    :return: DataFrame containing processed event data.
    :rtype: pd.DataFrame

    **Example usage for single match**:

    .. code-block:: python

        import pandas as pd
        from preprocessing import Event_data

        event_path='path/to/event.json'

        pff_fc_df=Event_data(data_provider='pff_fc',event_path=event_path).load_data()
        print(pff_fc_df.head())

    **Example usage for multiple matches**:

    .. code-block:: python

        from preprocessing import Event_data

        event_folder='path/to/event/folder'

        pff_fc_df=Event_data(data_provider='pff_fc',
                           event_path=event_folder,
                           max_workers=10).load_data()
        print(pff_fc_df.head())

    **Details**:

    This function reads PFF FC event data from a JSON file and converts it into a DataFrame. 
    
    1. Retrieves all event and tracking files from the input directories.
    2. Converts PFF-style event data to Metrica format.

    The returned DataFrame contains the following columns:

    - ``match_id``: Identifier for the match where the event occurred.
    - ``Team``: Team associated with the event ('Home' or 'Away')
    - ``Type``: Type of the event
    - ``Subtype``: Subtype of the event (e.g., 'success' or 'fail')
    - ``Period``: Period of the match (1 or 2)
    - ``Start Frame``: Frame index at event start
    - ``Start Time [s]``: Time in seconds at event start
    - ``End Frame``: Frame index at event end
    - ``End Time [s]``: Time in seconds at event end
    - ``From``: Player performing the action
    - ``To``: Player receiving the action (if applicable)
    - ``Start X``: Starting x-coordinate of the event
    - ``Start Y``: Starting y-coordinate of the event
    - ``End X``: Ending x-coordinate of the event
    - ``End Y``: Ending y-coordinate of the event

