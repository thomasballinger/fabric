============
Installation
============

Fabric is best installed via `pip <http://pip.openplans.org>`_ (highly
recommended) or `easy_install
<http://wiki.python.org/moin/CheeseShopTutorial>`_ (older, but still works
fine). You may also opt to use your operating system's package manager (the
package is typically called ``fabric`` or ``python-fabric``), or execute
``python setup.py install`` inside a :ref:`downloaded <downloads>` or
:ref:`cloned <source-code-checkouts>` copy of the source code.


Dependencies
============

In order for Fabric's installation to succeed, you will need four primary pieces of software:

* the Python programming language;
* the ``setuptools`` packaging/installation library;
* the PyCrypto cryptography library;
* and the Paramiko SSH2 library.

Please read on for important details on each dependency -- there are a few
gotchas.

Python
------

Fabric requires `Python <http://python.org>`_ version 2.5 or 2.6. Some caveats
and notes about other Python versions:

* We are not planning on supporting **Python 2.4** given its age and the number
  of useful tools in Python 2.5 such as context managers and new modules.
  That said, the actual amount of 2.5-specific functionality is not
  prohibitively large, and we would link to -- but not support -- a third-party
  2.4-compatible fork. (No such fork exists at this time, to our knowledge.)
* Fabric has not yet been tested on **Python 3.x** and is thus likely to be
  incompatible with that line of development. However, we try to be at least
  somewhat forward-looking (e.g. using ``print()`` instead of ``print``) and
  will definitely be porting to 3.x in the future once our dependencies do.

setuptools
----------

`Setuptools`_ comes with some Python installations by default; if yours doesn't,
you'll need to grab it. In such situations it's typically packaged as
``python-setuptools``, ``py25-setuptools`` or similar. Fabric may drop its
setuptools dependency in the future, or include alternative support for the
`Distribute`_ project, but for now setuptools is required for installation.

.. _setuptools: http://pypi.python.org/pypi/setuptools
.. _Distribute: http://pypi.python.org/pypi/distribute

PyCrypto
--------

`PyCrypto <http://www.amk.ca/python/code/crypto.html>`_ is a dependency of
Paramiko which provides the low-level (C-based) encryption algorithms used to
run SSH. There are a couple gotchas associated with installing PyCrypto: its
compatibility with Python's package tools, and the fact that it is a C-based
extension.

.. _pycrypto-and-pip:

Package tools
~~~~~~~~~~~~~

We strongly recommend using ``pip`` to install Fabric as it is newer and
generally better than ``easy_install``. However, a combination of bugs in
specific versions of Python, ``pip`` and PyCrypto can prevent installation of
PyCrypto. Specifically:

* Python = 2.5.x
* PyCrypto >= 2.1
* ``pip`` < 0.8.1

When all three criteria are met, you may encounter ``No such file or
directory`` IOErrors when trying to ``pip install Fabric`` or ``pip install
PyCrypto``.

The fix is simply to make sure at least one of the above criteria is not met,
by doing the following (in order of preference):

* Upgrade to ``pip`` 0.8.1 or above, e.g. by running ``pip install -U pip``.
* Explicitly install PyCrypto 2.0.1 (which is the latest version known to work with
  Fabric which does not cause the installation problem) via ``pip install
  PyCrypto==2.0.1``.
* Upgrade to Python 2.6 or above.


C extension
~~~~~~~~~~~

Unless you are installing from a precompiled source such as a Debian apt
repository or RedHat RPM, or using :ref:`pypm <pypm>`, you will also need the
ability to build Python C-based modules from source in order to install
PyCrypto. Users on **Unix-based platforms** such as Ubuntu or Mac OS X will
need the traditional C build toolchain installed (e.g. Developer Tools / XCode
Tools on the Mac, or the ``build-essential`` package on Ubuntu or Debian Linux
-- basically, anything with ``gcc``, ``make`` and so forth) as well as the
Python development libraries, often named ``python-dev`` or similar.

For **Windows** users we recommend using :ref:`pypm`, installing a C
development environment such as `Cygwin <http://cygwin.com>`_ or obtaining a
precompiled Win32 PyCrypto package from `voidspace's Python modules page
<http://www.voidspace.org.uk/python/modules.shtml#pycrypto>`_.

.. note::
    Some Windows users whose Python is 64-bit have found that the PyCrypto
    dependency ``winrandom`` may not install properly, leading to ImportErrors.
    In this scenario, you'll probably need to compile ``winrandom`` yourself
    via e.g. MS Visual Studio.  See :issue:`194` for info.

Development dependencies
------------------------

If you are interested in doing development work on Fabric (or even just running
the test suite), you may also need to install some or all of the following
packages:

* `git <http://git-scm.com>`_ and `Mercurial`_, in order to obtain some of the
  other dependencies below;
* `Nose <http://code.google.com/p/python-nose/>`_
* `Coverage <http://nedbatchelder.com/code/modules/coverage.html>`_
* `PyLint <http://www.logilab.org/857>`_
* `Fudge <http://farmdev.com/projects/fudge/index.html>`_
* `Sphinx <http://sphinx.pocoo.org/>`_

For an up-to-date list of exact testing/development requirements, including
version numbers, please see the ``requirements.txt`` file included with the
source distribution. This file is intended to be used with ``pip``, e.g. ``pip
install -r requirements.txt``.

.. _Mercurial: http://mercurial.selenic.com/wiki/


.. _downloads:

Downloads
=========

To obtain a tar.gz or zip archive of the Fabric source code, you may visit
either of the following locations:

* The official downloads are located in Fabric's Redmine instance at
  http://code.fabfile.org/projects/fabric/files/. This is the spot you want
  to download from for operating system packages, as the only changing part of
  the URL will be the filename itself and the md5 hashes will be consistent.
* Our `Git repository viewer <http://git.fabfile.org>`_ provides downloads of
  all tagged releases. See the "Download" column, next to the "Tag" column in
  the middle of the front page. Please note that due to how cgit generates tag
  archives, the md5 sums will change over time, so use of this location for
  package downloads is not recommended.
* `Our GitHub mirror <http://github.com/bitprophet/fabric>`_ also has downloads
  of all tagged releases -- just click the 'Download' button near the top of
  the main page.
* `Fabric's PyPI page <http://pypi.python.org/pypi/Fabric>`_ offers manual
  downloads in addition to being the entry point for ``pip`` and
  ``easy-install``.


.. _source-code-checkouts:

Source code checkouts
=====================

The Fabric developers manage the project's source code with the `Git
<http://git-scm.com>`_ DVCS. To follow Fabric's development via Git instead of
downloading official releases, you have the following options:

* Clone the canonical Git repository, ``git://fabfile.org/fabric.git`` (note
  that a Web view of this repository can be found at `git.fabfile.org
  <http://git.fabfile.org>`_)
* Clone the official Github mirror/collaboration repository,
  ``git://github.com/bitprophet/fabric.git``
* Make your own fork of the Github repository by making a Github account,
  visiting `GitHub/bitprophet/fabric <http://github.com/bitprophet/fabric>`_
  and clicking the "fork" button.

.. note::

    If you've obtained the Fabric source via source control and plan on
    updating your checkout in the future, we highly suggest using ``python
    setup.py develop`` instead -- it will use symbolic links instead of file
    copies, ensuring that imports of the library or use of the command-line
    tool will always refer to your checkout.

For information on the hows and whys of Fabric development, including which
branches may be of interest and how you can help out, please see the
:doc:`development` page.


.. _pypm:

ActivePython and PyPM
=====================

Windows users who already have ActiveState's `ActivePython
<http://www.activestate.com/activepython>`_ distribution installed may find
Fabric is best installed with its package manager, ``pypm``. Below is example
output from an installation of Fabric 0.9.0 via ``pypm``::

    C:\> pypm install fabric
    Ready to perform these actions:
    The following packages will be installed:
    fabric-0.9.0 pycrypto-2.0.1
    Get: [pypm.activestate.com] fabric 0.9.0-1
    Get: [pypm.activestate.com] pycrypto 2.0.1-1
    Installing fabric-0.9.0
    Fixing script
    C:\Users\<username>\AppData\Roaming\Python\Scripts\fab-script.py
    Installing pycrypto-2.0.1
