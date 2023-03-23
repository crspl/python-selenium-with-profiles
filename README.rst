================================
ADDITIONAL INFO FOR THIS VERSION
================================
This repository contains improved version of Python Selenium 3.14.1 with extra parameter allowing to reuse existing Firefox profile. When using this parameter then provider profile folder will be used directly and not copied to extra location like normally Selenium does. All cache / cookies etc will be available for next session. Changes are made on this version of Selenium and not the newest for few reasons: mainly it's for my purposes and I'm using older Selenium for backward compatibility but also newer Selenium requires newer Python what doesn't work for mee too. But in _patch folder there's patch with important changes so anybody can apply this (maybe with some modifications) to newer code

REQUIREMENTS:
    - geckodriver 0.32.2
    - Firefox 102.8

These versions were tested and work fine. Could be some older / newer (more likely) combinations will work too but it was not tested. For sure older gecko / FF don't use MarionetteActivePort file what is necessary for this to work

USAGE:
    from selenium import webdriver
    profile = webdriver.FirefoxProfile(profile_directory='/tmp/firefox-profile', reuse=True)
    driver = webdriver.Firefox(firefox_profile=profile)
    driver.get('https://www.google.com')
    driver.quit()

BEHAVIOUR:
    - profile_directory = None - fresh profile will be created
    - profile_directory set but folder doesn't exist - fresh profile will be created
    - profile_directory set and exists but reuse == False - standard behaviour - profile will be copied to new location and Firefox will use this copy. In the end copied profile folder will be removed
    - profile_directory set and exists and reuse == True - existing profile folder will be passed to Firefox and it will stay on disk after Firefox finishess

======================
Selenium Client Driver
======================

Introduction
============

Python language bindings for Selenium WebDriver.

The `selenium` package is used to automate web browser interaction from Python.

+-----------+--------------------------------------------------------------------------------------+
| **Home**: | http://www.seleniumhq.org                                                            |
+-----------+--------------------------------------------------------------------------------------+
| **Docs**: | `selenium package API <https://seleniumhq.github.io/selenium/docs/api/py/api.html>`_ |
+-----------+--------------------------------------------------------------------------------------+
| **Dev**:  | https://github.com/SeleniumHQ/Selenium                                               |
+-----------+--------------------------------------------------------------------------------------+
| **PyPI**: | https://pypi.org/project/selenium/                                                   |
+-----------+--------------------------------------------------------------------------------------+
| **IRC**:  | **#selenium** channel on freenode                                                    |
+-----------+--------------------------------------------------------------------------------------+

Several browsers/drivers are supported (Firefox, Chrome, Internet Explorer), as well as the Remote protocol.

Supported Python Versions
=========================

* Python 2.7, 3.4+

Installing
==========

If you have `pip <https://pip.pypa.io/>`_ on your system, you can simply install or upgrade the Python bindings::

    pip install -U selenium

Alternately, you can download the source distribution from `PyPI <https://pypi.org/project/selenium/#files>`_ (e.g. selenium-3.14.0.tar.gz), unarchive it, and run::

    python setup.py install

Note: You may want to consider using `virtualenv <http://www.virtualenv.org/>`_ to create isolated Python environments.

Drivers
=======

Selenium requires a driver to interface with the chosen browser. Firefox,
for example, requires `geckodriver <https://github.com/mozilla/geckodriver/releases>`_, which needs to be installed before the below examples can be run. Make sure it's in your `PATH`, e. g., place it in `/usr/bin` or `/usr/local/bin`.

Failure to observe this step will give you an error `selenium.common.exceptions.WebDriverException: Message: 'geckodriver' executable needs to be in PATH.`

Other supported browsers will have their own drivers available. Links to some of the more popular browser drivers follow.

+--------------+-----------------------------------------------------------------------+
| **Chrome**:  | https://sites.google.com/a/chromium.org/chromedriver/downloads        |
+--------------+-----------------------------------------------------------------------+
| **Edge**:    | https://developer.microsoft.com/en-us/microsoft-edge/tools/webdriver/ |
+--------------+-----------------------------------------------------------------------+
| **Firefox**: | https://github.com/mozilla/geckodriver/releases                       |
+--------------+-----------------------------------------------------------------------+
| **Safari**:  | https://webkit.org/blog/6900/webdriver-support-in-safari-10/          |
+--------------+-----------------------------------------------------------------------+

Example 0:
==========

* open a new Firefox browser
* load the page at the given URL

.. code-block:: python

    from selenium import webdriver

    browser = webdriver.Firefox()
    browser.get('http://seleniumhq.org/')

Example 1:
==========

* open a new Firefox browser
* load the Yahoo homepage
* search for "seleniumhq"
* close the browser

.. code-block:: python

    from selenium import webdriver
    from selenium.webdriver.common.keys import Keys

    browser = webdriver.Firefox()

    browser.get('http://www.yahoo.com')
    assert 'Yahoo' in browser.title

    elem = browser.find_element_by_name('p')  # Find the search box
    elem.send_keys('seleniumhq' + Keys.RETURN)

    browser.quit()

Example 2:
==========

Selenium WebDriver is often used as a basis for testing web applications.  Here is a simple example using Python's standard `unittest <http://docs.python.org/3/library/unittest.html>`_ library:

.. code-block:: python

    import unittest
    from selenium import webdriver

    class GoogleTestCase(unittest.TestCase):

        def setUp(self):
            self.browser = webdriver.Firefox()
            self.addCleanup(self.browser.quit)

        def testPageTitle(self):
            self.browser.get('http://www.google.com')
            self.assertIn('Google', self.browser.title)

    if __name__ == '__main__':
        unittest.main(verbosity=2)

Selenium Server (optional)
==========================

For normal WebDriver scripts (non-Remote), the Java server is not needed.

However, to use Selenium Webdriver Remote or the legacy Selenium API (Selenium-RC), you need to also run the Selenium server.  The server requires a Java Runtime Environment (JRE).

Download the server separately, from: http://selenium-release.storage.googleapis.com/3.14/selenium-server-standalone-3.14.0.jar

Run the server from the command line::

    java -jar selenium-server-standalone-3.14.0.jar

Then run your Python client scripts.

Use The Source Luke!
====================

View source code online:

+-----------+-------------------------------------------------------+
| official: | https://github.com/SeleniumHQ/selenium/tree/master/py |
+-----------+-------------------------------------------------------+
