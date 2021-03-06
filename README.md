# WordPress

[![Build Status](https://travis-ci.org/miya0001/wpdev.svg?branch=master)](https://travis-ci.org/miya0001/wpdev)

This is a private development repository for WordPress

## How to mirror SVN

```
$ mkdir wpdev && cd wpdev
$ git svn clone -s --prefix=svn/ http://develop.svn.wordpress.org .
$ git remote add origin git@github.com:miya0001/wpdev.git
$ git push origin --all
```

## How to sync

```
$ git checkout master
$ git svn rebase
$ git push origin --all
```

## How to create patch

Create a working branch:

```
$ git checkout master
$ git checkout -b my-patch
```

Commit:

```
$ git add .
$ git commit -m "Some fix"
```

Create a patch:

```
$ git diff master --no-prefix
```

## How to run phpunit

To setup, run following commands:

```
git checkout master
mysql -u root -e "CREATE DATABASE wordpress_tests;"
cp wp-tests-config-sample.php wp-tests-config.php
sed -i -e "s/youremptytestdbnamehere/wordpress_tests/" wp-tests-config.php
sed -i -e "s/yourusernamehere/root/" wp-tests-config.php
sed -i -e "s/yourpasswordhere//" wp-tests-config.php
npm install
$(npm bin)/grunt
svn checkout https://plugins.svn.wordpress.org/wordpress-importer/tags/0.6.3/ tests/phpunit/data/plugins/wordpress-importer
```

Then run `phpunit`.