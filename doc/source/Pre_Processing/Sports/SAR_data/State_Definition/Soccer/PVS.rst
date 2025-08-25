PVS State Definition
=======================

Overview
--------

PVS (Position and Velocity State) is a simple state definition system designed for multi-agent reinforcement learning applications. It focuses on basic position and action information and is applied to applications where simple state representation is sufficient.

Data Structure
--------------

PVS has the following simple hierarchical structure:

.. code-block:: python

    class State_PVS(BaseModel):
        ball: Ball
        players: List[Player]
        attack_players: List[Player] 
        defense_players: List[Player]

Components
----------

Ball
~~~~

Basic ball information:

* **position**: Ball position information (x, y coordinates)
* **velocity**: Ball velocity information

Player
~~~~~~

Basic player information:

* **index**: Player index
* **team_name**: Team name
* **player_name**: Player name
* **player_id**: Player ID  
* **player_role**: Player position
* **position** : Player position information (x, y coordinates)
* **velocity**: Player velocity information
* **action**: Player action
* **action_probs**: Probability of action occurrence

Attack/Defense Players
~~~~~~~~~~~~~~~~~~~~~~
Separate management of player lists during attack and defense

Action Structure
~~~~~~~~~~~~~~~~

PVS assigns a single action to each player:

.. code-block:: python

    action: List[str]  # One action per player

Processing Flow
---------------

Main Processing Functions

1. **frames2events_pvs()**
   
   - Conversion from frame data to event data
   - Simple processing pipeline
   - Basic event extraction

2. **frame2state_pvs()**
   
   - Conversion from frame data to PVS state
   - Basic state extraction processing
   - Structuring of player and ball information

Usage
-----

Example of using the PVS system:

.. code-block:: python

    SAR_data = SAR_data(
        data_provider="fifawc",
        state_def="PVS",          # Specify PVS state definition
        data_path=data_path,
        match_id="3814",
        preprocess_method="SAR"
    )

Application Scenarios
----------------------

PVS is suitable for the following applications:

* **Basic reinforcement learning**: Learning tasks where simple state representation is sufficient
* **Prototyping**: Cases requiring rapid development and testing
* **Educational purposes**: Learning and understanding multi-agent systems
* **Resource constraints**: Environments with limited computational resources

Technical Limitations
---------------------

* Does not include advanced tactical analysis functions
* No support for spatial control or formation analysis
* Not suitable for complex interaction modeling


File Structure
--------------

Main PVS-related files:

* ``SAR_class.py``: Factory class for PVS/EDMS switching
* ``dataclass.py``: PVS data class definitions
* ``preprocess_frame.py``: PVS processing functions
* ``soccer_SAR_state.py``: Main processing routing for PVS

Summary
-------

PVS is a lightweight system optimized for multi-agent reinforcement learning applications that require simple state representation. It focuses on basic position and action information with a design that emphasizes fast processing and ease of understanding.