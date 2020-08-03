Introduction
============

.. image:: https://readthedocs.org/projects/adafruit-circuitpython-vectorprogressbar/badge/?version=latest
    :target: https://circuitpython.readthedocs.io/projects/vectorprogressbar/en/latest/
    :alt: Documentation Status

.. image:: https://img.shields.io/discord/327254708534116352.svg
    :target: https://adafru.it/discord
    :alt: Discord

.. image:: https://github.com/adafruit/Adafruit_CircuitPython_VectorProgressBar/workflows/Build%20CI/badge.svg
    :target: https://github.com/adafruit/Adafruit_CircuitPython_VectorProgressBar/actions
    :alt: Build Status

.. image:: https://img.shields.io/badge/code%20style-black-000000.svg
    :target: https://github.com/psf/black
    :alt: Code Style: Black

Vector based dynamic progress bar widget for CircuitPython displays. Intended to be a drop-in replacement for https://github.com/adafruit/Adafruit_CircuitPython_ProgressBar usable on devices with support for vectorio.


Dependencies
=============
This driver depends on:

* `Adafruit CircuitPython <https://github.com/adafruit/circuitpython>`_

Please ensure all dependencies are available on the CircuitPython filesystem.
This is easily achieved by downloading
`the Adafruit library and driver bundle <https://circuitpython.org/libraries>`_.

Installing from PyPI
=====================
.. note:: This library is not available on PyPI yet. Install documentation is included
   as a standard element. Stay tuned for PyPI availability!

Usage Example
=============

.. code:: python

    import time
    import board
    import displayio
    from adafruit_vector_progressbar import ProgressBar

    # Make the display context
    splash = displayio.Group(max_size=10)
    board.DISPLAY.show(splash)

    # set progress bar width and height relative to board's display
    width = board.DISPLAY.width-40
    height = 30

    x = board.DISPLAY.width // 2 - width // 2
    y = board.DISPLAY.height // 3

    # Create a new progress_bar object at (x, y)
    progress_bar = ProgressBar(x, y, width, height, 1.0)

    # Append progress_bar to the splash group
    splash.append(progress_bar)

    current_progress = 0.0
    while True:
        # range end is exclusive so we need to use 1 bigger than max number that we want
        for current_progress in range(0, 101, 1):
            print("Progress: {}%".format(current_progress))
            progress_bar.progress = current_progress / 100  # convert to decimal
            time.sleep(0.01)
        time.sleep(0.3)
        progress_bar.progress = 0.0
        time.sleep(0.3)

Contributing
============

Contributions are welcome! Please read our `Code of Conduct
<https://github.com/adafruit/Adafruit_CircuitPython_VectorProgressBar/blob/master/CODE_OF_CONDUCT.md>`_
before contributing to help this project stay welcoming.

Documentation
=============

For information on building library documentation, please check out `this guide <https://learn.adafruit.com/creating-and-sharing-a-circuitpython-library/sharing-our-docs-on-readthedocs#sphinx-5-1>`_.
