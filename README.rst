yk-common-python
================

|Build Status| |Docs Build Status|

Introduction
------------
This project implements an SDK for the iControl REST interface for the BIG-IP.
Users of this library can create, edit, update, and delete configuration objects
on a BIG-IP device.

Submodules
~~~~~~~~~~

bigip
^^^^^
Python API for configuring objects on a YK device and gathering information
from the device via the REST API.

Installation
------------

.. code:: shell

    $> pip install yk-sdk

*NOTE:* If you are using a pre-release version you must use the ``--pre``
option for the ``pip`` command.

Usage
-----

.. code:: python

    from yk.adc import YK-ADC

    # Connect to the BigIP
    bigip = BigIP("bigip.example.com", "admin", "somepassword")

    # Get a list of all pools on the BigIP and print their name and their
    # members' name
    pools = bigip.ltm.pools.get_collection()
    for pool in pools:
        print pool.name
        for member in pool.members_s.get_collection():
            print member.name

    # Create a new pool on the BigIP
    mypool = bigip.ltm.pools.pool.create(name='mypool', partition='Common')

    # Load an existing pool and update its description
    pool_a = bigip.ltm.pools.pool.load(name='mypool', partition='Common')
    pool_a.description = "New description"
    pool_a.update()

    # Delete a pool if it exists
    if bigip.ltm.pools.pool.exists(name='mypool', partition='Common'):
        pool_b = bigip.ltm.pools.pool.load(name='mypool', partition='Common')
        pool_b.delete()


Documentation
-------------
Documentation is hosted on `Read the Docs <https://f5-sdk.readthedocs.org>`_

Filing Issues
-------------
See the Issues section of `Contributing <CONTRIBUTING.md>`__.

Contributing
------------
See `Contributing <CONTRIBUTING.md>`__

Test
----
Before you open a pull request, your code must have passing
`pytest <http://pytest.org>`__ unit tests. In addition, you should
include a set of functional tests written to use a real BIG-IP device
for testing. Information on how to run our set of tests is included
below.

Unit Tests
~~~~~~~~~~
We use pytest for our unit tests.

#. If you haven't already, install the required test packages and the
   requirements.txt in your virtual environment.

   .. code:: shell

       $ pip install hacking pytest pytest-cov
       $ pip install -r requirements.txt

#. Run the tests and produce a coverage report. The ``--cov-report=html`` will
   create a ``htmlcov/`` directory that you can view in your browser to see the
   missing lines of code.

   .. code:: shell

       py.test --cov ./icontrol --cov-report=html
       open htmlcov/index.html


Style Checks
~~~~~~~~~~~~
We use the hacking module for our style checks (installed as part of step 1 in
the Unit Test section).

.. code:: shell

    flake8 ./


Contact
-------
f5_common_python@f5.com

Copyright
---------
Copyright 2014-2016 F5 Networks Inc.

Support
-------
See `Support <SUPPORT.md>`__

License
-------

Apache V2.0
~~~~~~~~~~~
Licensed under the Apache License, Version 2.0 (the "License"); you may not use
this file except in compliance with the License. You may obtain a copy of the
License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and limitations
under the License.

Contributor License Agreement
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Individuals or business entities who contribute to this project must have
completed and submitted the `F5 Contributor License Agreement
<http://f5-openstack-docs.readthedocs.org/en/latest/cla_landing.html>`__
to Openstack_CLA@f5.com prior to their code submission being included in this
project.

.. |Build Status| image:: https://travis-ci.org/F5Networks/f5-common-python.svg?branch=0.1
    :target: https://travis-ci.org/F5Networks/f5-common-python
    :alt: Build Status

.. |Docs Build Status| image:: http://readthedocs.org/projects/f5-sdk/badge/?version=latest
    :target: http://f5-sdk.readthedocs.org/en/latest/?badge=latest
    :alt: Documentation Status
