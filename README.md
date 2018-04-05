Markdown Benchmarks (PHP)
=========================

[![Build Status](https://travis-ci.org/kzykhys/Markbench.png?branch=master)](https://travis-ci.org/kzykhys/Markbench)
[![Latest Stable Version](https://poser.pugx.org/kzykhys/markbench/v/stable.png)](https://packagist.org/packages/kzykhys/markbench)
[![SensioLabsInsight](https://insight.sensiolabs.com/projects/f85a4034-6089-4b14-acb5-990e202a5a55/mini.png)](https://insight.sensiolabs.com/projects/f85a4034-6089-4b14-acb5-990e202a5a55)

All parsers are managed by composer (minimum-stability=stable).
Tested with latest stable version.

[**See the latest benchmark on Travis-CI**](https://travis-ci.org/kzykhys/Markbench)

```
$ php bin/markbench benchmark --profile=github-sample
Runtime: PHP7.0.8
Host:    Linux cebe-desktop 3.16.0-5-amd64 #1 SMP Debian 3.16.51-3+deb8u1 (2018-01-08) x86_64
Profile: Sample content from Github (http://github.github.com/github-flavored-markdown/sample_content.html) / 1000 times
Class:   Markbench\Profile\GithubSampleProfile

+------------------------+---------+------------+---------------+----------+--------------+
| package                | version | dialect    | duration (MS) | MEM (B)  | PEAK MEM (B) |
+------------------------+---------+------------+---------------+----------+--------------+
| erusev/parsedown       | 1.7.1   |            | 1293          | 14680064 | 14680064     |
| cebe/markdown          | 1.2.1   |            | 1412          | 14680064 | 14680064     |
| cebe/markdown          | 1.2.1   | extra      | 1626          | 14680064 | 14680064     |
| cebe/markdown          | 1.2.1   | gfm        | 1873          | 14680064 | 14680064     |
| michelf/php-markdown   | 1.8.0   |            | 2179          | 14680064 | 14680064     |
| erusev/parsedown-extra | 0.7.1   | extra      | 2328          | 14680064 | 14680064     |
| michelf/php-markdown   | 1.8.0   | extra      | 3098          | 14680064 | 14680064     |
| kzykhys/ciconia        | v1.0.2  |            | 3239          | 14680064 | 14680064     |
| kzykhys/ciconia        | v1.0.2  | gfm        | 3973          | 14680064 | 14680064     |
| league/commonmark      | 0.17.5  | commonmark | 6953          | 14680064 | 14680064     |
+------------------------+---------+------------+---------------+----------+--------------+
```

Tested parsers
--------------

* [michelf/php-markdown](https://github.com/michelf/php-markdown) [![Latest Stable Version](https://poser.pugx.org/michelf/php-markdown/v/stable.png)](https://packagist.org/packages/michelf/php-markdown)
* [kzykhys/ciconia](https://github.com/kzykhys/Ciconia) [![Latest Stable Version](https://poser.pugx.org/kzykhys/ciconia/v/stable.png)](https://packagist.org/packages/kzykhys/ciconia)
* [erusev/parsedown](https://github.com/erusev/parsedown) [![Latest Stable Version](https://poser.pugx.org/erusev/parsedown/v/stable.png)](https://packagist.org/packages/erusev/parsedown)
* [erusev/parsedown-extra](https://github.com/erusev/parsedown-extra) [![Latest Stable Version](https://poser.pugx.org/erusev/parsedown-extra/v/stable.png)](https://packagist.org/packages/erusev/parsedown-extra)
* [cebe/markdown](https://github.com/cebe/markdown) [![Latest Stable Version](https://poser.pugx.org/cebe/markdown/v/stable.png)](https://packagist.org/packages/cebe/markdown)
* [league/commonmark](https://github.com/thephpleague/commonmark) [![Latest Stable Version](https://poser.pugx.org/league/commonmark/v/stable.png)](https://packagist.org/packages/league/commonmark)

Internals
---------

Each parser is executed asynchronously using [kzykhys/Parallel.php](https://github.com/kzykhys/Parallel.php)

```
Runner
 +-->(kzykhys/Parallel.php)
        +-- child process #1 --+
        +-- child process #2 --+--> output
        +-- child process #3 --+
        |-- duration/mem usage --|
```

### Requirements

* PHP5.4+
* Compiled with --enable-pcntl

Add a parser
------------

* Put your class that implements `Markbench\DriverInterface` into `Driver` directory.
* Run command again

**Feel free to fork and send a pull request!**

Run a benchmark
---------------

```
composer install
bin/markbench benchmark
```

```
$ bin/markbench help benchmark
Usage:
 benchmark [--parser="..."] [-p|--profile[="..."]]

Options:
 --parser              Name of a parser. Available: cebe/markdown, cebe/markdown:gfm, kzykhys/ciconia, kzykhys/ciconia:gfm, erusev/parsedown, michelf/php-markdown, michelf/php-markdown:extra
 --profile (-p)        Name of a profile. (default: "default")
 --help (-h)           Display this help message.
 --quiet (-q)          Do not output any message.
 --verbose (-v|vv|vvv) Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug
 --version (-V)        Display this application version.
 --ansi                Force ANSI output.
 --no-ansi             Disable ANSI output.
 --no-interaction (-n) Do not ask any interactive question.
```

### Profiles

* default
* blank
* github-sample

### Add a profile

* Put your class that implements `Markbench\ProfileInterface` into `Profile` directory.
* Run `php bin/markbench benchmark --profile=your_profile_name`

**Feel free to fork and send a pull request!**

License
-------

The MIT License

Author
------

Kazuyuki Hayashi (@kzykhys)
