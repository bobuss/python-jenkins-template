# Jenkins python template

Use those files to scaffold your Continuous Integration Server with your python projects.

This was inspirated by [the PHP jenkins template project](http://jenkins-php.org/) ([github](https://github.com/sebastianbergmann/php-jenkins-template)).



## Requirements

* [SLOCCount](http://www.dwheeler.com/sloccount/)

        $ (sudo) apt-get install sloccount

* [pylint](http://pypi.python.org/pypi/pylint)

        $ (sudo) pip install pylint

* [Clone Digger](http://clonedigger.sourceforge.net/)

        $ (sudo) easy_install clonedigger

* [nosetests](http://readthedocs.org/docs/nose/en/latest/) & [nosexcover](http://pypi.python.org/pypi/nosexcover)

        $ (sudo) pip install nosetests
        $ (sudo) pip install nosexcover

* [pyflakes](http://pypi.python.org/pypi/pyflakes)

        $ (sudo) pip install pyflakes


## Jenkins Plugins

* [Jenkins SLOCCount Plug-in](http://wiki.jenkins-ci.org/display/JENKINS/SLOCCount+Plugin)
* [Jenkins xUnit plugin](http://wiki.jenkins-ci.org/display/JENKINS/xUnit+Plugin)
* [Jenkins Violations plugin](http://wiki.jenkins-ci.org/display/JENKINS/Violations)
* [Warnings Plug-in](https://wiki.jenkins-ci.org/display/JENKINS/Warnings+Plugin)
* [Cobertura plugin](https://wiki.jenkins-ci.org/display/JENKINS/Cobertura+Plugin)


## Jenkins (sort of) configuration

Install the hudson.plugins.warnings.WarningsPublisher.xml file on the jenkins server.

Or, If you prefer to click :

1.  Go to Manage Jenkins -> Configure System
2.  Scroll down to Compiler Warnings -> Parsers
3.  Add a new parser with the following details:

    1.  Name and others descriptive fields:

            PyFlakes

    2.  Regular Expression:

            ^\s*(.*):(\d+):\s*(.*)$

    3.  Mapping Script:

            import hudson.plugins.warnings.parser.Warning

            String fileName = matcher.group(1)
            String lineNumber = matcher.group(2)
            String message = matcher.group(3)

            return new Warning(fileName, Integer.parseInt(lineNumber), "Dynamic Parser", "-", message);

    4.  Example Log Message:

            src/fbproxy/fbresponse.py:2: 'json' imported but unused


## In your project

Get the Makefile and adapt it (source directory, tasks). Make sure to generate the right files (or change the config):

* pyflakes.log
* pylint.log
* sloccount.sc
* output.xml
* coverage.xml
* xunit.xml


## Some other resources

* [http://www.wallix.org/2011/06/29/how-to-use-jenkins-for-python-development/](http://www.wallix.org/2011/06/29/how-to-use-jenkins-for-python-development/)
* [http://www.alexconrad.org/2011/10/jenkins-and-python.html](http://www.alexconrad.org/2011/10/jenkins-and-python.html)

