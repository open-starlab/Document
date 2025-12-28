BePro (SoccerTrackv2)
=====================

.. py:class:: Phase_data(data_provider='bepro', event_path=None, bp_tracking_json_paths=None, bp_tracking_xml_path=None, meta_data=None)

     Load and process event and tracking data for the BePro (SoccerTrackv2) dataset. 
     This class supports both modern JSON-based tracking sequences and legacy XML tracking files.

     :param str data_provider: Name of the data provider (default is 'bepro').
     :param str event_path: File path to the BePro event CSV file.
     :param list bp_tracking_json_paths: (For Match ID >= 130000) A list of paths to JSON frame data files.
     :param str bp_tracking_xml_path: (For Match ID < 130000) File path to the tracker box XML data.
     :param str meta_data: File path to the match metadata (JSON or XML depending on the match ID).
     :return: A synchronized DataFrame containing processed phase data.
     :rtype: pandas.DataFrame

    **Example Usage**:

     Depending on the Match ID, the data structure differs. The following example shows the conditional loading logic.

     .. code-block:: python

          import os
          import glob
          from preprocessing import Phase_data

          match_id = "130001"
          data_provider = 'bepro'
          base_dir = '/path/to/data'

          if int(match_id) >= 130000:
               # New Format (JSON)
               file_pattern = os.path.join(base_dir, 'tracking_data', data_provider, match_id, f"{match_id}_*_frame_data.json")
               tracking_json_paths = sorted(glob.glob(file_pattern))
               meta_data = os.path.join(base_dir, 'tracking_data', data_provider, match_id, f"{match_id}_metadata.json")
               event_csv_path = glob.glob(os.path.join(base_dir, 'event_data', data_provider, match_id, '*.csv'))[0]

               preprocessing_df = Phase_data(
                    data_provider=data_provider, 
                    bp_tracking_json_paths=tracking_json_paths, 
                    event_path=event_csv_path, 
                    meta_data=meta_data
               ).load_data()
          else:
               # Old Format (XML)
               tracking_path = os.path.join(base_dir, 'tracking_data', data_provider, match_id, f"{match_id}_tracker_box_data.xml")
               meta_data = os.path.join(base_dir, 'tracking_data', data_provider, match_id, f"{match_id}_tracker_box_metadata.xml")
               event_csv_path = glob.glob(os.path.join(base_dir, 'event_data', data_provider, match_id, '*.csv'))[0]

               preprocessing_df = Phase_data(
                    data_provider=data_provider, 
                    bp_tracking_xml_path=tracking_path, 
                    event_path=event_csv_path, 
                    meta_data=meta_data
               ).load_data()

          # Save the standardized output
          output_file_path = os.path.join(base_dir, 'phase_data', data_provider, match_id, f"{match_id}_main_data.csv")
          preprocessing_df.to_csv(output_file_path, index=False)

    **Details**:

     The BePro processing pipeline unifies disparate data sources into a standardized coordinate system:

    1. **Format Detection**: Automatically handles JSON sequences for newer matches and XML files for legacy data.
    2. **Metadata Integration**: Extracts pitch dimensions, team rosters, and player details from metadata files.
    3. **Time Synchronization**: Merges tracking frames with event data using the nearest time-match logic.
    4. **Feature Extraction**: 
          - Normalizes position coordinates.
          - Adds ball-specific tracking columns.
          - Organizes player data (id, name, position, x, y) for both home and away teams.
    5. **Downsampling**: Standardizes the output to 5fps (200ms) to ensure consistency across the OpenSTARLab ecosystem.