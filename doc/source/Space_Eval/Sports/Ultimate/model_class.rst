Space_Model Class
=========================
This class provides a framework for ultimate events space evaluation, including the calculation and visualization of space model.

Initialization
----------------------------
.. class:: Space_Model(space_model, event_data=None, tracking_home=None, tracking_away=None, out_path=None, testing_mode=False)

   Initializes the wUPPCF calculator.

   :param space_model: (str) Name of the space model to use (e.g., 'wUPPCF').
   :param event_data: (str or pd.DataFrame) Path to event CSV file/folder.
   :param tracking_home: (str or pd.DataFrame) Path to home team tracking CSV file/folder.
   :param tracking_away: (str or pd.DataFrame) Path to away team tracking CSV file/folder.
   :param provider: (str) Data provider name (e.g., 'UltimateTrack', 'UFA').
   :param out_path: (str, optional) Directory to save wUPPCF results and visualizations. Defaults to None.
   :param testing_mode: (bool, optional) If True, only a limited number of frames/events will be processed. Defaults to False.
Methods
--------------
.. method:: read_data()

   Reads the event and tracking data. Supports both single CSV files and directories containing multiple CSV files.
   Returns dictionaries mapping match IDs to their respective DataFrames.

   :return: Tuple of dictionaries `(event_dict, tracking_home_dict, tracking_away_dict)`.

.. method:: get_wuppcf()

   Calculates the wUPPCF for all matches in the dataset. Saves the results to the `out_path` if specified.

   :return: Dictionary mapping match IDs to the results dictionary named WUPPCFResult `(wuppcf, player_wuppcf, events_metric, tracking_home_metric, tracking_away_metric)`.

.. method:: vis_wuppcf(WUPPCFResult)

   Visualizes the wUPPCF for a specific possession on a ultimate pitch. Saves the video to `out_path` if specified.

   :param WUPPCFResult: (dict) The wUPPCF result dictionary obtained from `get_wuppcf()`.

