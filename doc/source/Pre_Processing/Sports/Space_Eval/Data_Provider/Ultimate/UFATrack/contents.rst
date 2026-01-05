UFATrack
============================================
.. class:: Space_data(data_provider='UFATrack', tracking_data_path=tracking_data_path, out_path=None, testing_mode=False).preprocessing() -> pd.DataFrame

    Load the UFATrack from csv files(s) and convert it into a DataFrame.

    :param tracking_data_path: Path to the csv file/folder containing tracking data.
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

        tracking_path = './UFATrack/Tracking Data'
        out_path = './'

        Space_data(data_provider='UFATrack',
                tracking_data_path=tracking_path,
                out_path=out_path
                ).preprocessing()

    **Details**

    This function performs the following steps:

    1. Retrieves all tracking files from the input directories using `get_files()`.
    2. Converts raw tracking data into an intermediate DataFrames using `create_intermediate_file`.
    3. Converts intermediate DataFrames into fixed-format home and away tracking DataFrames and event DataFrames using `convert_to_metrica_format`.
    4. Convert the multi-index tracking columns into a single-row header using `format_tracking_headers`.
    5. Organizes results into dictionaries keyed by match ID:

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
        - ``Home_1_x`` … ``Home_7_x``: X-coordinates of home players 1–7
        - ``Home_1_y`` … ``Home_7_y``: Y-coordinates of home players 1–7
        - ``disc_x``: Disc X-coordinate
        - ``disc_y``: Disc Y-coordinate

    - **Away Tracking DataFrame (`away_tracking_dict[match_id]`)**:
        - ``Period``: Period of the match (1 or 2)
        - ``Time [s]``: Time in seconds
        - ``Away_1_x`` … ``Away_7_x``: X-coordinates of away players 1–7
        - ``Away_1_y`` … ``Away_7_y``: Y-coordinates of away players 1–7
        - ``disc_x``: Disc X-coordinate
        - ``disc_y``: Disc Y-coordinate