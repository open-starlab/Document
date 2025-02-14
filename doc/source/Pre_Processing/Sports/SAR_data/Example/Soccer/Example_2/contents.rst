Download and Preprocess StatsBomb and SkillCorner Data
======================================================

This script downloads StatsBomb event and match data, matches it with SkillCorner tracking data, and processes the combined data.

Dependencies
------------

* `os`
* `json`
* `tqdm`
* `pandas`
* `openstarlab_preprocessing`

Usage
-----

.. code-block:: python
    
    import os
    import json
    from tqdm import tqdm
    import pandas as pd
    from statsbombpy import sb

    from preprocessing import SAR_data

    #down_load_statsbomb_data function
    def download_statsbomb_data(creds, save_dir,competition_id=11, season_id=281):

        os.makedirs(save_dir, exist_ok=True)

        def convert_df_in_dict(d):
            for key, value in d.items():
                if isinstance(value, pd.DataFrame):
                    d[key] = value.to_dict(orient='records')
                elif isinstance(value, dict):
                    convert_df_in_dict(value)
            return d

        # Get Statsbomb matches data
        matches = sb.matches(competition_id=competition_id, season_id=season_id, creds=creds)
        matches["competition_id"] = competition_id
        matches["season_id"] = season_id
        #moev the competition_id and season_id to the first column
        cols = matches.columns.tolist()
        cols = cols[-2:] + cols[:-2]
        matches = matches[cols]
        #save the matches to csv
        matches.to_csv(os.path.join(save_dir, "matches.csv"), index=False)

        # Get Statsbomb lineups and events
        os.makedirs(os.path.join(save_dir, "lineups"), exist_ok=True)
        os.makedirs(os.path.join(save_dir, "events"), exist_ok=True)
        for match_id in tqdm(matches["match_id"].unique()):
            lineups = sb.lineups(match_id=match_id, creds=creds)
            events = sb.events(match_id=match_id, include_360_metrics=True, creds=creds)
            events.to_csv(os.path.join(save_dir, "events", f"{match_id}.csv"), index=False)
            #save the lineups as json and with row changes
            lineups = convert_df_in_dict(lineups)
            with open(os.path.join(save_dir, "lineups", f"{match_id}.json"), "w") as f:
                json.dump(lineups, f, indent=4)

    if __name__ == "__main__":
        #Statsbomb API
        creds = {"user": "input your Statsbomb api user name here", "passwd": "input your Statsbomb api password here"}
        #Statsbomb event data saving dir
        save_dir = "/statsbomb"
        #path to the skillcorner tracking data
        tracking_path="/skillcorner/tracking"
        #path to the skillcorner match data
        match_path="/skillcorner/match"

        download_statsbomb_data(creds, save_dir)


        #Match the statsbomb and skillcorner (one file)
        data_path = save_dir+'/events'
        match_id = "1120811"
        config_path = '/path/to/preprocess_config.json'
        statsbomb_skillcorner_match_id = '/path/to/statsbomb_skillcorner_match_id.json'

        #Load single match data
        Soccer_SAR_data(
            data_provider='statsbomb_skillcorner',
            data_path=data_path,
            match_id=match_id, # match_id for skillcorner
            config_path=config_path,
            statsbomb_skillcorner_match_id=statsbomb_skillcorner_match_id,
        ).load_data()

        #Match the statsbomb and skillcorner (multiple files)
        config_path = '/path/to/preprocess_config.json'
        statsbomb_skillcorner_match_id = '/path/to/statsbomb_skillcorner_match_id.json'

        #Load multiple matches data
        Soccer_SAR_data(
            data_provider='statsbomb_skillcorner',
            data_path=data_path,
            config_path=config_path,
            statsbomb_skillcorner_match_id=statsbomb_skillcorner_match_id,
            max_workers=2
        ).load_data()

        # Preprocess the statsbomb and skillcorner data (single file)
        Soccer_SAR_data(
            data_provider='statsbomb_skillcorner',
            data_path=data_path,
            match_id=match_id,
            config_path=config_path,
            preprocess_method="SAR"
        ).preprocess_single_data(
            cleaning_dir=os.getcwd()+"/data/stb_skc/clean_data",
            preprocessed_dir=os.getcwd()+"/data/stb_skc/preprocess_data"
        )

        # Preprocess the statsbomb and skillcorner data (multiple files)
        Soccer_SAR_data(
            data_provider='statsbomb_skillcorner',
            data_path=data_path,
            config_path=config_path,
            preprocess_method="SAR"
        ).preprocess_multiple_data(
            cleaning_dir=os.getcwd()+"/data/stb_skc/clean_data",
            preprocessed_dir=os.getcwd()+"/data/stb_skc/preprocess_data"
        )

        print("---------------done-----------------")