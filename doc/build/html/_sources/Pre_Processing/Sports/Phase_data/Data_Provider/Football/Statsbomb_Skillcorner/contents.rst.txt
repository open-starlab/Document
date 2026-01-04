StatsBomb & SkillCorner Integration
====================================

.. py:class:: Phase_data(data_provider='statsbomb_skillcorner', sb_event_path=None, sc_tracking_path=None, sc_match_path=None, sc_players_path=None)

    Load and synchronize StatsBomb event data with SkillCorner tracking data to generate standardized phase data.

    :param str data_provider: Name of the data provider (default is 'statsbomb_skillcorner').
    :param str sb_event_path: File path to the StatsBomb event data (.pkl).
    :param str sc_tracking_path: File path to the SkillCorner tracking data (.json).
    :param str sc_match_path: File path to the SkillCorner match metadata (.json).
    :param str sc_players_path: File path to the SkillCorner players master data (.json).
    :return: A synchronized and structured DataFrame.
    :rtype: pd.DataFrame

    **Example Usage**:

    The following example demonstrates how to process a single match by specifying the direct paths to the data files.

    .. code-block:: python

        import os
        from preprocessing import Phase_data

        # Define Match IDs
        sb_match_id = 3894537
        sc_match_id = 1018887
        data_provider = 'statsbomb_skillcorner'
        base_dir = 'D:/lab/My_Research/Github/OpenSTARLab/PreProcessing/test/'

        # Construct File Paths
        sb_event_path = f'{base_dir}/sports/event_data/statsbomb/{sb_match_id}_events.pkl'
        sc_tracking_path = f'{base_dir}/sports/tracking_data/skillcorner/LaLiga-2023-2024/tracking/{sc_match_id}.json'
        sc_match_path = f'{base_dir}/sports/tracking_data/skillcorner/LaLiga-2023-2024/match/{sc_match_id}.json'
        sc_players_path = f'{base_dir}/sports/tracking_data/skillcorner/LaLiga-2023-2024/players/players.json'

        # Initialize and Load Data
        preprocessing_df = Phase_data(
            data_provider=data_provider, 
            sb_event_path=sb_event_path, 
            sc_tracking_path=sc_tracking_path, 
            sc_match_path=sc_match_path, 
            sc_players_path=sc_players_path
        ).load_data()

        # Save Processed Data
        output_file_dir = os.path.join(base_dir, 'phase_data', data_provider, f'{sb_match_id}_{sc_match_id}')
        os.makedirs(output_file_dir, exist_ok=True)
        output_file_path = os.path.join(output_file_dir, f"{sb_match_id}_{sc_match_id}_main_data.csv")
        
        preprocessing_df.to_csv(output_file_path, index=False)

    **Data Processing Workflow**:

    The ``load_data()`` method executes the following steps to ensure data consistency:

    1. **Metadata Extraction**: Parses the SkillCorner match and player JSON files to map IDs to player names and positions.
    2. **Coordinate Normalization**: Determines the attacking direction for each team (Left/Right) and normalizes coordinates based on the team attacking the positive x-axis.
    3. **In-Play Detection**: Analyzes StatsBomb events to identify continuous "in-play" sequences, assigning a unique ``inplay_num`` to each sequence.
    4. **Temporal Alignment**: Synchronizes the SkillCorner tracking timestamps with StatsBomb event timestamps, adjusting for period-based time resets.
    5. **Sampling**: Downsamples the tracking data to 5fps (200ms intervals) to optimize for machine learning model input.
    6. **Ordering**: Sorts players within each team (1 to 11) according to the position hierarchy (GK → DF → MF → FW).