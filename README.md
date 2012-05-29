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

* Jenkins SLOCCount Plug-in
* Jenkins xUnit plugin
* Jenkins Violations plugin
* Warnings Plug-in


## Jenkins (sort of) configuration

Install the hudson.plugins.warnings.WarningsPublisher.xml file on the jenkins server.


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

