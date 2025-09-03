Space_Model Class
=========================
This class provides a framework for soccer events space evaluation, including the calculation and visualization of space model.

Initialization
--------------
.. class:: Space_Model(space_model, event_data=None, tracking_home=None, tracking_away=None, out_path=None, testing_mode=False)

   Initializes the OBSO calculator.

   :param space_model: (str) Name of the space model to use (e.g., 'soccer_OBSO').
   :param event_data: (str or pd.DataFrame) Path to event CSV file/folder.
   :param tracking_home: (str or pd.DataFrame) Path to home team tracking CSV file/folder.
   :param tracking_away: (str or pd.DataFrame) Path to away team tracking CSV file/folder.
   :param out_path: (str, optional) Directory to save OBSO results and visualizations. Defaults to None.
   :param testing_mode: (bool, optional) If True, only a limited number of frames/events will be processed. Defaults to False.
Methods
-------
.. method:: read_data()

   Reads the event and tracking data. Supports both single CSV files and directories containing multiple CSV files.  
   Returns dictionaries mapping match IDs to their respective DataFrames.

   :return: Tuple of dictionaries `(event_dict, tracking_home_dict, tracking_away_dict)`.

.. method:: get_obso()

   Calculates the OBSO for all matches in the dataset. Saves the results to the `out_path` if specified.

   :return: Dictionary mapping match IDs to the results tuple `(home_obso, away_obso, home_onball_obso, away_onball_obso, PPCF_dict)`.

.. method:: vis_obso(event_id, events_data, tracking_home, tracking_away, PPCF, out_path=None)

   Visualizes the OBSO for a specific event on a soccer pitch. Saves the figure to `out_path` if specified.

   :param event_id: (int or str) ID of the event (not row) to visualize.
   :param events_data: (str or pd.DataFrame) Event data CSV file/folder or DataFrame.
   :param tracking_home: (str or pd.DataFrame) Home tracking CSV file/folder or DataFrame.
   :param tracking_away: (str or pd.DataFrame) Away tracking CSV file/folder or DataFrame.
   :param PPCF: (str or dict) Precomputed PPCF dictionary file (numpy `.npy`) or dict.
   :param out_path: (str, optional) Directory to save the visualization. Defaults to `self.out_path` if provided.
   :return: Matplotlib figure and axis `(fig, ax)`.

