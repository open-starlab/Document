Other Event Data Formats
========================

The following methods replicate the event data format designed for specific models in the existing literature. The data format is designed to be compatible with the model's input requirements and to facilitate the analysis of football event data.

For more information on the specific models and their data formats, refer to the references provided below. For the implementation of these data formats, refer to the respective example below.

Method: NMSTPP
--------------

The Transformer-Based Neural Marked Spatio Temporal Point Process (NMSTPP) model is a comprehensive approach designed to handle large-scale spatiotemporal data, particularly in the context of football event data.

Example for a single file::

    import pandas as pd
    from preprocessing import Event_data

    event_path = 'path/to/event_data.csv'
    match_path = 'path/to/match_data.csv'
    max_workers = 1

    wyscout_df = Event_data(data_provider='wyscout', event_path=event_path, wyscout_matches_path=match_path, preprocess_method="NMSTPP", max_workers=max_workers).preprocessing()
    print(wyscout_df.head())

Example for multiple files::

    import pandas as pd
    from preprocessing import Event_data

    event_folder = 'path/to/event/folder'
    match_folder = 'path/to/match/folder'
    max_workers = 1

    wyscout_df = Event_data(data_provider='wyscout', event_path=event_folder, wyscout_matches_path=match_folder, preprocess_method="SEQ2EVENT", max_workers=10).preprocessing()
    print(wyscout_df.head())

Reference:

.. code-block:: text

    @article{yeung2023transformer,
      title={Transformer-based neural marked spatio temporal point process model for football match events analysis},
      author={Yeung, Calvin CK and Sit, Tony and Fujii, Keisuke},
      journal={arXiv preprint arXiv:2302.09276},
      year={2023}
    }

Method: Seq2Event
-----------------

Seq2Event is a model designed to predict the next event in a sequence of events within a given context, specifically tailored for analyzing dynamic sports like soccer. The model leverages Transformer or Recurrent Neural Network (RNN) components to handle the complexity of player actions and roles which occur simultaneously and at multiple temporal scales with high spatial freedom.

Example for a single file::

    import pandas as pd
    from preprocessing import Event_data

    event_path = 'path/to/event_data.csv'
    match_path = 'path/to/match_data.csv'
    max_workers = 1

    wyscout_df = Event_data(data_provider='wyscout', event_path=event_path, wyscout_matches_path=match_path, preprocess_method="SEQ2EVENT", max_workers=max_workers).preprocessing()
    print(wyscout_df.head())

Example for multiple files::

    import pandas as pd
    from preprocessing import Event_data

    event_folder = 'path/to/event/folder'
    match_folder = 'path/to/match/folder'
    max_workers = 1

    wyscout_df = Event_data(data_provider='wyscout', event_path=event_path, wyscout_matches_path=match_folder, preprocess_method="NMSTPP", max_workers=10).preprocessing()
    print(wyscout_df.head())

Reference:

.. code-block:: text

    @inproceedings{simpson2022seq2event,
      title={Seq2event: learning the language of soccer using transformer-based match event prediction},
      author={Simpson, Ian and Beal, Ryan J and Locke, Duncan and Norman, Timothy J},
      booktitle={Proceedings of the 28th ACM SIGKDD Conference on Knowledge Discovery and Data Mining},
      pages={3898--3908},
      year={2022}
    }

Method: LEM
-----------

The Large Event Model (LEM) is a comprehensive machine-learning model designed to predict and analyze events within a specific domain, such as soccer matches. Unlike traditional models that often simplify event dynamics by abstracting or relying on a combination of sequential models, LEMs aim to predict the entire chain of variables that constitute an event. This holistic approach allows LEMs to offer several advantages.

Example for a single file::

    import pandas as pd
    from preprocessing import Event_data

    event_path = 'path/to/event_data.csv'
    match_path = 'path/to/match_data.csv'
    max_workers = 1

    wyscout_df = Event_data(data_provider='wyscout', event_path=event_path, wyscout_matches_path=match_path, preprocess_method="LEM", max_workers=max_workers).preprocessing()
    print(wyscout_df.head())

Example for multiple files::

    import pandas as pd
    from preprocessing import Event_data

    event_folder = 'path/to/event/folder'
    match_folder = 'path/to/match/folder'
    max_workers = 1

    wyscout_df = Event_data(data_provider='wyscout', event_path=event_folder, wyscout_matches_path=match_folder, preprocess_method="LEM", max_workers=10).preprocessing()
    print(wyscout_df.head())

Reference:

.. code-block:: text

    @article{mendes2024forecasting,
      title={Forecasting Events in Soccer Matches Through Language},
      author={Mendes-Neves, Tiago and Meireles, Lu{\'\i}s and Mendes-Moreira, Jo{\~a}o},
      journal={arXiv preprint arXiv:2402.06820},
      year={2024}
    }
