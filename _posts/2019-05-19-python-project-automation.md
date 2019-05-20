---
layout: post
title: Python Project Automation (Github Badges!)
tags: [python, readthedocs, tox, travis, coveralls, coverage, pytest]
image: img/posts/2019-05-19-python-project-automation/preview.jpg
---

There's a number of free services available to help automating aspects of a Python project if it's stored on [github](https://github.com/):

* [Read the Docs](https://readthedocs.org/) for building and hosting documentation.
* [pytest](https://docs.pytest.org/en/latest/) for running tests.
* [tox](https://tox.readthedocs.io/en/latest/) for testing deployed code rather than development code.
* [coverage.py](https://coverage.readthedocs.io/en/latest/index.html) for measuring the coverage of tests.
* [coveralls.io](https://coveralls.io/) for tracking coverage.
* [Travis](https://travis-ci.org/) for running builds and tests.

By connecting your github account to these services and making some configuration files in your project it's quite easy to improve your project and get fancy github badges as a reward!

I wanted to:

* Build documentation locally for testing
* Build and host documentation on Read the Docs
* Run my tests locally
* Generate a coverage report locally
* Run tests on Travis
* Generate coverage reports on Travis
* Track coverage using coveralls.io
* Get fancy github badges

Documentation
-------------

Testing and Coverage
--------------------

Travis and Coveralls
--------------------

Badges
------

Lessons Learned
---------------

If things aren't syncing up or your getting error messages, try logging out and back in to everything then refreshing/resyncing if the service provides that functionality.