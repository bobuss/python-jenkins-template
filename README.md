# Jenkins python template

Use these files to scaffold your Continuous Integration Server within your python projects.

This was inspirated by [the PHP jenkins template project](http://jenkins-php.org/) ([github](https://github.com/sebastianbergmann/php-jenkins-template)) by Sebastian Bergmann.



## Requirements

On your jenkins instance, you must install some QA python tools:

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

You also need to install some plugins in your jenkins server:

* [Jenkins SLOCCount Plug-in](http://wiki.jenkins-ci.org/display/JENKINS/SLOCCount+Plugin)
* [Jenkins xUnit plugin](http://wiki.jenkins-ci.org/display/JENKINS/xUnit+Plugin)
* [Jenkins Violations plugin](http://wiki.jenkins-ci.org/display/JENKINS/Violations)
* [Warnings Plug-in](https://wiki.jenkins-ci.org/display/JENKINS/Warnings+Plugin)
* [Cobertura plugin](https://wiki.jenkins-ci.org/display/JENKINS/Cobertura+Plugin)


## Jenkins configuration

Install the hudson.plugins.warnings.WarningsPublisher.xml file on the jenkins server, then reload the configuration.

Or, if you prefer to click in the web interface:

1. Go to Manage Jenkins -> Configure System
2. Scroll down to Compiler Warnings -> Parsers
3. Add a new parser with the following details:

    1. Name and others descriptive fields:

            PyFlakes

    2. Regular Expression:

            ^\s*(.*):(\d+):\s*(.*)$

    3. Mapping Script:

            import hudson.plugins.warnings.parser.Warning

            String fileName = matcher.group(1)
            String lineNumber = matcher.group(2)
            String message = matcher.group(3)

            return new Warning(fileName, Integer.parseInt(lineNumber), "Dynamic Parser", "-", message);

    4.  Example Log Message:

            src/fbproxy/fbresponse.py:2: 'json' imported but unused


## Using the Job Template

1. Check out the `python-jenkins-template` project from Git:

        cd $JENKINS_HOME/jobs
        git clone git://github.com/bobuss/python-jenkins-template.git python-template
        chown -R jenkins:nogroup python-template/

2. Reload Jenkins' configuration, for instance using the Jenkins CLI:

        java -jar jenkins-cli.jar -s http://<jenkins_address>:<jenkins_port> reload-configuration

3. Click on "New Job".

4. Enter a "Job name".

5. Select "Copy existing job" and enter "python-template" into the "Copy from" field.

6. Click "OK".

7. Disable the "Disable Build" option.

8. Fill in your "Source Code Management" information.

9. Configure a "Build Trigger", for instance "Poll SCM".

10. Click "Save".


## In your project

Get the `Makefile` and adapt it (source directory, tasks). Make sure to generate the right files (or change the jenkins config):

* pyflakes.log
* pylint.log
* sloccount.sc
* output.xml
* coverage.xml
* xunit.xml

You can also adapt your `.gitignore` file, in order to avoid to commit the generated files.


## Some other resources

* [http://www.wallix.org/2011/06/29/how-to-use-jenkins-for-python-development/](http://www.wallix.org/2011/06/29/how-to-use-jenkins-for-python-development/)
* [http://www.alexconrad.org/2011/10/jenkins-and-python.html](http://www.alexconrad.org/2011/10/jenkins-and-python.html)


## License

(The MIT License)

Copyright (c) 2012 Bertrand Tornil <bertrand.tornil@gmail.com>

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the 'Software'), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.


