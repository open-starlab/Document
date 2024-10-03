Models and Framework
=============================================

The following framework and models are designed to predict and analyze events in football/soccer matches. Unlike traditional models that often simplify event dynamics by abstracting or relying on a combination of sequential models, these models aim to predict the entire chain of variables that constitute an event. 

The models in this package has been edited to be compatible with the framework specified below. For more information on the specific models, refer to the references provided below. For data format and preprocessing, refer to the `Pre-Processing <https://github.com/open-starlab/PreProcessing>`_ package.

Framework
---------
TBA

Pre-Trained Models
------------------
The following models are available for use in predicting soccer match events:

TBA

The yaml file for the pre-trained models can be found `here <https://github.com/open-starlab/Event/tree/main/event/sports/soccer/models/model_yaml>`_.

Models: NMSTPP
------------------
The Transformer-Based Neural Marked Spatio Temporal Point Process (NMSTPP) model is designed to handle the complex spatiotemporal dynamics of football match event data. Leveraging the neural temporal point processes (NTPP) framework, the model captures both the timing and spatial information of events, enabling more accurate predictions of future actions in a match. 

.. code-block:: text

    @article{yeung2023transformer,
      title={Transformer-based neural marked spatio temporal point process model for football match events analysis},
      author={Yeung, Calvin CK and Sit, Tony and Fujii, Keisuke},
      journal={arXiv preprint arXiv:2302.09276},
      year={2023}
    }


Models: Seq2Event
------------------
Seq2Event model, which leverages Transformer or RNN components to provide a holistic approach to match event prediction. Predicting the next event based on prior actions and contextual information.

.. code-block:: text

    @inproceedings{simpson2022seq2event,
      title={Seq2event: learning the language of soccer using transformer-based match event prediction},
      author={Simpson, Ian and Beal, Ryan J and Locke, Duncan and Norman, Timothy J},
      booktitle={Proceedings of the 28th ACM SIGKDD Conference on Knowledge Discovery and Data Mining},
      pages={3898--3908},
      year={2022}
    }


Models: FMS
------------
The Foundation Model for Soccer (FMS) is a deep learning framework designed to predict subsequent actions in soccer matches based on a sequence of prior actions.

.. code-block:: text

    @article{baron2024foundation,
        title={A Foundation Model for Soccer},
        author={Baron, Ethan and Hocevar, Daniel and Salehe, Zach},
        journal={arXiv preprint arXiv:2407.14558},
        year={2024}
    }


Models: LEM
------------
The Large Events Model (LEM) for soccer is a deep learning framework designed to simulate soccer matches from a given game state. Its primary function is to generate probabilities and outcomes for various events based on multiple simulations. 

.. code-block:: text

    @article{mendes2024forecasting,
      title={Forecasting Events in Soccer Matches Through Language},
      author={Mendes-Neves, Tiago and Meireles, Lu{\'\i}s and Mendes-Moreira, Jo{\~a}o},
      journal={arXiv preprint arXiv:2402.06820},
      year={2024}
    }

    @article{mendes2024towards,
      title={Towards a foundation large events model for soccer},
      author={Mendes-Neves, Tiago and Meireles, Lu{\'\i}s and Mendes-Moreira, Jo{\~a}o},
      journal={Machine Learning},
      pages={1--23},
      year={2024},
      publisher={Springer}
    }

Models: MAJ
------------------
The Majority-class model (MAJ) is a simple baseline model that predicts the most frequent event class in the training data. This model is used to establish a baseline for comparison with more complex models.