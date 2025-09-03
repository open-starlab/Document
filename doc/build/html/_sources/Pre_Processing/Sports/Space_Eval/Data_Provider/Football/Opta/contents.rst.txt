Opta
==============
.. class:: Event_data(data_provider='opta',event_path=opta_f24_path,match_id=match_id).load_data()

    Loads Opta XML data and converts it into a pandas DataFrame.

    :param f24_path: The file path to the Opta f24 XML file.
    :type f24_path: str
    :param match_id: The ID of the match. Defaults to None.
    :type match_id: str, optional
    :return: A DataFrame containing event data.
    :rtype: pd.DataFrame

    **Example usage**:

    .. code-block:: python

        import pandas as pd
        from preprocessing import Event_data

        opta_f24_path = 'path/to/opta_f24.xml'
        match_id='12345'
        opta_df=Event_data(data_provider='opta',event_path=opta_f24_path,match_id=match_id).load_data()
        print(opta_df.head())

    **Details**:

    This function parses the given Opta f24 XML file to extract event data for a specific match. The event data is then organized into a pandas DataFrame with the following steps:

    1. The XML file is parsed to get the root element.
    2. An empty list is initialized to store the event details.
    3. Each event in the XML is iterated through to extract relevant details such as period, minute, second, event type, outcome, team, and coordinates.
    4. These details are appended to the event list.
    5. The event list is converted into a pandas DataFrame with specified columns.
    6. The minute and second columns are combined into a total seconds column for easier sorting.
    7. The DataFrame is sorted by the total seconds column and the columns are reordered.


    The returned DataFrame contains the following columns:

    - ``match_id``: The ID of the match.
    - ``period``: The period of the match in which the event occurred.
    - ``minute``: The minute in the match at which the event occurred.
    - ``second``: The second in the match at which the event occurred.
    - ``total_seconds``: The total time in seconds from the start of the match.
    - ``event_type``: The primary type of the event.
    - ``event_type_2``: The secondary type of the event.
    - ``outcome``: The outcome of the event.
    - ``team``: The ID of the team associated with the event.
    - ``start_x``: The starting x-coordinate of the event on the pitch.
    - ``start_y``: The starting y-coordinate of the event on the pitch.



