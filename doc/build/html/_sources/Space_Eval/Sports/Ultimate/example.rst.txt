Example: Calculate and Visualize wUPPCF
=============================================
To calculate and visualize the weighted Ultimate Pitch Control Field (wUPPCF) [Iwashita, 2024] using the ``Space_Model``, you can utilize the following code snippets.


Calculate wUPPCF
---------------------------

.. code-block:: python

    from spaceeval import Space_Model

    event_path = './event'
    home_tracking_path = './home_tracking'
    away_tracking_path = './away_tracking'
    out_path = './'

    model = Space_Model(space_model='wUPPCF',
                event_data=event_path,
                tracking_home=home_tracking_path,
                tracking_away=away_tracking_path,
                out_path=out_path)

    results = model.get_wuppcf()


Visualize wUPPCF
--------------------

After calculating wUPPCF, you can visualize it. Here’s how to do it:

.. code-block:: python

    from spaceeval import Space_Model

    model.vis_wuppcf(results)

Example Visualization
---------------------------------------------------

The Visualization results for the wUPPCF should look like this:

.. image:: wuppcf.png
    :alt: wUPPCF visualization
    :width: 876px
    :height: 355px
    :align: center