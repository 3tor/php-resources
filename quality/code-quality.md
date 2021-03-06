---
title: "Writing Quality Code and Code Analysis"
updated: "October 9, 2016"
permalink: "/article/testing-and-quality/php-and-code-quality/"
redirect_from: "/faq/testing-and-quality/php-and-code-quality/"
---

Beside writing tests, there are more factors that affect the quality of your
code. Let's check some tools for PHP that can improve your code quality.

## PhpMetrics

![PhpMetrics](/images/quality/phpmetrics.png "PhpMetrics")

[PhpMetrics][phpmetrics] is a very convenient static analysis tool for your
code and your PHP projects.

It can be installed with [Composer][composer] or by downloading [phar][phar]:

```bash
composer global require 'halleck45/phpmetrics'
phpmetrics --report-html=myreport.html /path/of/your/sources
```

PhpMetrics can even interact with [Jenkins][Jenkins] and [Sonar][sonar].

After running PhpMetrics from terminal you get an HTML file that looks
something like this:

![PhpMetrics Report](/images/quality/phpmetrics_2.png "PhpMetrics Report")

Some examples of PhpMetrics reports:

* [CodeIgniter 3.0 PhpMetrics report](http://bl.ocks.org/peterkokot/raw/c5b4da6935d9a8684248/)
* [Symfony 2.6 PhpMetrics report](http://bl.ocks.org/peterkokot/raw/d43726688595f112a419/)

## Resources

Other useful tools to check out:

* [PHP Parser][phpparser] - This is a PHP 5.2 to PHP 7.1 parser written in PHP. Its purpose is to simplify static code analysis and manipulation.
* [PHP QA tools][phpqatools] - List of PHP Quality Assurance tools
* [Jenkins PHP][jenkinsphp] - Template for Jenkins Jobs for PHP Projects
* [PHP Mess Detector][phpmd] - User friendly and easy to configure frontend for the raw metrics measured by [PHP Depend][phpdepend]
* [PHPCheckStyle][phpcheckstyle] - open-source tool that helps PHP programmers adhere to certain coding conventions
* [Qafoo Quality Analyzer](https://github.com/Qafoo/QualityAnalyzer) - Tool helping us to analyze software projects.

[phpparser]: https://github.com/nikic/PHP-Parser
[phpmetrics]: http://phpmetrics.org
[phar]: https://github.com/Halleck45/PhpMetrics/raw/master/build/phpmetrics.phar
[jenkins]: http://jenkins-ci.org/
[sonar]: http://www.sonarqube.org
[phpqatools]: http://phpqatools.org/
[jenkinsphp]: http://jenkins-php.org/
[phpmd]: http://phpmd.org/
[phpdepend]: http://pdepend.org/
[phpcheckstyle]: https://phpcheckstyle.github.io/
[composer]: https://getcomposer.org/
