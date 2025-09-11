FIFA WC 2022 (PFF format)
============================================
.. class:: Space_data(data_provider='fifa_wc_2022').load_data() -> pd.DataFrame

    Load the FIFA WC 2022 event data and tracking from JSON file(s) and bz2 files(s) and convert it into a DataFrame.

    :param event_data_path: Path to the json file/folder containing event data.
    :type event_data_path: str

    :param tracking_data_path: Path to the bz2 file/folder containing tracking data.
    :type tracking_data_path: str

    :param out_path: Path to the output folder where processed data will be saved.
    :type out_path: str, optional

    :param testing_mode: If True, run in testing mode with limited data.
    :type testing_mode: bool, optional

    :returns: `(event_data_dict, home_tracking_dict, away_tracking_dict)` — dictionaries mapping match IDs to respective DataFrames.
    :rtype: tuple of dict

    **Example**

    .. code-block:: python

        from preprocessing import Space_data

        event_path = './FIFA_WC_2022/Event Data'
        tracking_path = './FIFA_WC_2022/Tracking Data'
        out_path = './'

        Space_data(data_provider='fifa_wc_2022',
                event_data_path=event_path,
                tracking_data_path=tracking_path,
                out_path=out_path
                ).preprocessing()

    **Details**

    This function performs the following steps:

    1. Retrieves all event and tracking files from the input directories using `get_files()`.
    2. Converts PFF-style event data to Metrica format for each match using `convert_pff2metrica`.
    3. Converts raw tracking data into fixed-format home and away tracking DataFrames using `convert_tracking_data_fixed_ids`.
    4. Organizes results into dictionaries keyed by match ID:
    
       - `event_data_dict` for event DataFrames
       - `home_tracking_dict` for home team tracking DataFrames
       - `away_tracking_dict` for away team tracking DataFrames

    The returned DataFrames include the following columns:

    - **Event DataFrame (`event_data_dict[match_id]`)**:
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

    - **Home Tracking DataFrame (`home_tracking_dict[match_id]`)**:
        - ``Period``: Period of the match (1 or 2)
        - ``Time [s]``: Time in seconds
        - ``Home_1_x`` … ``Home_16_x``: X-coordinates of home players 1–16
        - ``Home_1_y`` … ``Home_16_y``: Y-coordinates of home players 1–16
        - ``ball_x``: Ball X-coordinate
        - ``ball_y``: Ball Y-coordinate

    - **Away Tracking DataFrame (`away_tracking_dict[match_id]`)**:
        - ``Period``: Period of the match (1 or 2)
        - ``Time [s]``: Time in seconds
        - ``Away_1_x`` … ``Away_16_x``: X-coordinates of away players 1–16
        - ``Away_1_y`` … ``Away_16_y``: Y-coordinates of away players 1–16
        - ``ball_x``: Ball X-coordinate
        - ``ball_y``: Ball Y-coordinate
