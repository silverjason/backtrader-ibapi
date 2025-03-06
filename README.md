# Backtrader-IBAPI Fork

This is a public fork of Backtrader, a Python backtesting and trading library, modified to integrate with Interactive Brokers' IBAPI.

Backtrader uses IbPy package for live tading with IBAPI, however that package is no longer supported hence the need to rather use IBKR's official API package.

## License

This project is licensed under the **GNU General Public License v3.0 (GPL-3.0)**, as inherited from the original [Backtrader project](https://www.backtrader.com/).

### Inclusion of BSD-Licensed Code

Some portions of this repository may include code originally developed by Atreyu Group LLC, which is licensed under the **BSD 2-Clause License**. This BSD-licensed code remains under its original terms, but since this project as a whole is licensed under **GPL-3.0**, all distributed versions of this fork must comply with GPL-3.0 requirements.

For details on GPL-3.0, see the LICENSE file in this repository or visit GNU's website.

## Attribution

* **Backtrader**: Originally developed by Daniel Rodriguez and licensed under GPL-3.0.
* **Atreyu Group LLC**: Some IBAPI-related improvements in this fork originate from BSD-licensed code.

## Contribution

By contributing to this repository, you agree that your contributions will also be licensed under GPL-3.0 to maintain compatibility with the Backtrader project.


backtrader
==========

.. image:: https://img.shields.io/pypi/v/backtrader.svg
   :alt: PyPi Version
   :scale: 100%
   :target: https://pypi.python.org/pypi/backtrader/

..  .. image:: https://img.shields.io/pypi/dm/backtrader.svg
       :alt: PyPi Monthly Donwloads
       :scale: 100%
       :target: https://pypi.python.org/pypi/backtrader/

.. image:: https://img.shields.io/pypi/l/backtrader.svg
   :alt: License
   :scale: 100%
   :target: https://github.com/backtrader/backtrader/blob/master/LICENSE
.. image:: https://travis-ci.org/backtrader/backtrader.png?branch=master
   :alt: Travis-ci Build Status
   :scale: 100%
   :target: https://travis-ci.org/backtrader/backtrader
.. image:: https://img.shields.io/pypi/pyversions/backtrader.svg
   :alt: Python versions
   :scale: 100%
   :target: https://pypi.python.org/pypi/backtrader/

**Yahoo API Note**:

  [2018-11-16] After some testing it would seem that data downloads can be
  again relied upon over the web interface (or API ``v7``)

**Tickets**

  The ticket system is (was, actually) more often than not abused to ask for
  advice about samples.

For **feedback/questions/...** use the `Community <https://community.backtrader.com>`_

Here a snippet of a Simple Moving Average CrossOver. It can be done in several
different ways. Use the docs (and examples) Luke!
::

  from datetime import datetime
  import backtrader as bt

  class SmaCross(bt.SignalStrategy):
      def __init__(self):
          sma1, sma2 = bt.ind.SMA(period=10), bt.ind.SMA(period=30)
          crossover = bt.ind.CrossOver(sma1, sma2)
          self.signal_add(bt.SIGNAL_LONG, crossover)

  cerebro = bt.Cerebro()
  cerebro.addstrategy(SmaCross)

  data0 = bt.feeds.YahooFinanceData(dataname='MSFT', fromdate=datetime(2011, 1, 1),
                                    todate=datetime(2012, 12, 31))
  cerebro.adddata(data0)

  cerebro.run()
  cerebro.plot()

Including a full featured chart. Give it a try! This is included in the samples
as ``sigsmacross/sigsmacross2.py``. Along it is ``sigsmacross.py`` which can be
parametrized from the command line.

Features:
=========

Live Trading and backtesting platform written in Python.

  - Live Data Feed and Trading with

    - Interactive Brokers (needs ``ibapi`` and benefits greatly from an
      installed ``pytz``)
    - *Visual Chart* (needs a fork of ``comtypes`` until a pull request is
      integrated in the release and benefits from ``pytz``)
    - *Oanda* (needs ``oandapy``) (REST API Only - v20 did not support
      streaming when implemented)

  - Data feeds from csv/files, online sources or from *pandas* and *blaze*
  - Filters for datas, like breaking a daily bar into chunks to simulate
    intraday or working with Renko bricks
  - Multiple data feeds and multiple strategies supported
  - Multiple timeframes at once
  - Integrated Resampling and Replaying
  - Step by Step backtesting or at once (except in the evaluation of the Strategy)
  - Integrated battery of indicators
  - *TA-Lib* indicator support (needs python *ta-lib* / check the docs)
  - Easy development of custom indicators
  - Analyzers (for example: TimeReturn, Sharpe Ratio, SQN) and ``pyfolio``
    integration (**deprecated**)
  - Flexible definition of commission schemes
  - Integrated broker simulation with *Market*, *Close*, *Limit*, *Stop*,
    *StopLimit*, *StopTrail*, *StopTrailLimit*and *OCO* orders, bracket order,
    slippage, volume filling strategies and continuous cash adjustmet for
    future-like instruments
  - Sizers for automated staking
  - Cheat-on-Close and Cheat-on-Open modes
  - Schedulers
  - Trading Calendars
  - Plotting (requires matplotlib)

Documentation
=============

The blog:

  - `Blog <http://www.backtrader.com/blog>`_

Read the full documentation at:

  - `Documentation <http://www.backtrader.com/docu>`_

List of built-in Indicators (122)

  - `Indicators Reference <http://www.backtrader.com/docu/indautoref.html>`_

Python 2/3 Support
==================

  - Python >= ``3.2``

  - It also works with ``pypy`` and ``pypy3`` (no plotting - ``matplotlib`` is
    not supported under *pypy*)

Installation
============

``backtrader`` is self-contained with no external dependencies (except if you
want to plot)

From *pypi*:

  - ``pip install backtrader``

  - ``pip install backtrader[plotting]``

    If ``matplotlib`` is not installed and you wish to do some plotting

.. note:: The minimum matplotlib version is ``1.4.1``

An example for *IB* Data Feeds/Trading:

  - Please install the ibapi package separately https://interactivebrokers.github.io/

For other functionalities like: ``Visual Chart``, ``Oanda``, ``TA-Lib``, check
the dependencies in the documentation.

From source:

  - Place the *backtrader* directory found in the sources inside your project

Version numbering
=================

X.Y.Z.I

  - X: Major version number. Should stay stable unless something big is changed
    like an overhaul to use ``numpy``
  - Y: Minor version number. To be changed upon adding a complete new feature or
    (god forbids) an incompatible API change.
  - Z: Revision version number. To be changed for documentation updates, small
    changes, small bug fixes
  - I: Number of Indicators already built into the platform
