Models and Framework
=============================================

The following framework and models are designed to serve as a foundational framework for implementing reward models in soccer decision-making analysis.

The models in this package has been edited to be compatible with the framework specified below. For more information on the specific models, refer to the references provided below. For data format and preprocessing, refer to the `Pre-Processing <https://github.com/open-starlab/PreProcessing>`_ package.

Framework
---------
The data were then converted to the `SAR format <https://openstarlab.readthedocs.io/en/latest/Pre_Processing/Sports/Event_data/Data_Format/Football/UEID.html>`_ using the OpenSTARLab `Pre-Processing <https://github.com/open-starlab/PreProcessing>`_ package. Afterward, all models were trained with the OpenSTARLab RLearn package. For more details refer to our paper.

.. code-block:: text

    @article{yeung2025openstarlab,
        title={OpenSTARLab: Open Approach for Spatio-Temporal Agent Data Analysis in Soccer},
        author={Yeung, Calvin and Ide, Kenjiro and Someya, Taiga and Fujii, Keisuke},
        journal={arXiv preprint arXiv:2502.02785},
        year={2025}
    }


Model: sarsa_attacker
----------------------
The sarsa_attacker model serves as a foundational framework for implementing reward models in soccer decision-making analysis. Designed to evaluate and assign rewards based on specific game situations, this class provides a structured approach to integrating domain-specific reward functions into reinforcement learning models. By leveraging spatiotemporal data, it enables a more interpretable assessment of player decisions and tactical effectiveness.

.. code-block:: text

    @article{nakahara2023action,
        title={Action valuation of on-and off-ball soccer players based on multi-agent deep reinforcement learning},
        author={Nakahara, Hiroshi and Tsutsui, Kazushi and Takeda, Kazuya and Fujii, Keisuke},
        journal={IEEE Access},
        volume={11},
        pages={131237--131244},
        year={2023},
        publisher={IEEE}
    }